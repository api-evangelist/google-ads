---
name: google-ads-launch-search-campaign
description: >-
  Create a budget, campaign, ad group, keywords and an ad in Google Ads — the full launch
  chain, with a dry run first. This skill SPENDS MONEY; it must not run unattended.
api: Google Ads API
apiId: google-ads:google-ads-api
version: v25
spec: openapi/google-ads-api-v25-openapi.yml
operations:
  - googleads_customers_campaignBudgets_mutate
  - googleads_customers_campaigns_mutate
  - googleads_customers_adGroups_mutate
  - googleads_customers_adGroupCriteria_mutate
  - googleads_customers_adGroupAds_mutate
  - googleads_customers_googleAds_mutate
consequence: write
human_in_the_loop: required
generated: '2026-08-13'
method: generated
source: >-
  openapi/google-ads-api-v25-openapi.yml (operationIds verified against the spec),
  conventions/google-ads-conventions.yml, data-model/google-ads-data-model.yml
---

# Launch a Google Ads search campaign

Five objects, in dependency order: budget → campaign → ad group → criteria → ad. Each is
created by a `:mutate` operation carrying an `operations` array.

**This changes live advertising spend.** The Google Ads API has no idempotency key: a
retried mutate that already succeeded creates a second campaign. Get a human decision
before the first non-`validateOnly` call, and record the resource names you get back.

## Steps

1. **Dry run everything first.** Send each mutate below with `validateOnly: true`. The
   server runs full validation and applies nothing. Fix every error before proceeding.

2. **Create the budget.** `googleads_customers_campaignBudgets_mutate`
   (`POST /v25/customers/{customersId}/campaignBudgets:mutate`). `amountMicros` is in
   micros of the account currency — 50000000 is 50.00. Note the returned resource name.

3. **Create the campaign.** `googleads_customers_campaigns_mutate`. Reference the budget's
   resource name in `campaignBudget`. Set `advertisingChannelType`, `status` (start
   `PAUSED` — see below), and the bidding strategy.

4. **Create the ad group.** `googleads_customers_adGroups_mutate`, with `campaign` set to
   the campaign resource name.

5. **Add keywords.** `googleads_customers_adGroupCriteria_mutate`, with `adGroup` set and
   one operation per keyword (text + match type).

6. **Add the ad.** `googleads_customers_adGroupAds_mutate`, with `adGroup` set and the ad
   payload inline. `googleads_customers_ads_mutate` updates an existing ad's creative;
   creating a NEW ad inside an ad group goes through `adGroupAds:mutate`.

## Do it in one call instead

`googleads_customers_googleAds_mutate`
(`POST /v25/customers/{customersId}/googleAds:mutate`) accepts operations across all of
these resource types in a single atomic request. Use **temp ids** — negative ids that act
as forward references — so the campaign can point at a budget created in the same request:

```
mutateOperations:
  - campaignBudgetOperation: { create: { resourceName: "customers/{cid}/campaignBudgets/-1", ... } }
  - campaignOperation:       { create: { campaignBudget: "customers/{cid}/campaignBudgets/-1", ... } }
```

This is the safer shape for a launch: one request either lands entirely or not at all,
which is as close to idempotent as this API gets.

## Rules that will bite you

- **Start PAUSED.** Create the campaign with `status: PAUSED`, verify it in the UI, then
  enable it deliberately. An ENABLED campaign starts spending immediately.
- **`partialFailure` cuts both ways.** With it true, valid operations apply and invalid
  ones come back in a `partial_failure_error` keyed by index — useful for bulk keywords,
  dangerous for a launch chain where a half-built campaign is worse than none. Leave it
  false for steps 2–6.
- **Updates need `updateMask`.** Omitted fields are left alone, not cleared.
- **Ceilings.** 10,000 mutate operations per request, 100 action operations per request.
  Above that, use BatchJobService (`googleads_customers_batchJobs_mutate` and friends).
- **No rollback.** There is no undo. Removing a campaign you just created is another
  mutate, and the spend that already happened stays.

## Errors worth handling

`REQUIRED_FIELD_MISSING` (the `location` field names the exact path) ·
`RESOURCE_NOT_FOUND` (a referenced resource name is wrong — read them back from a search,
never construct them) · `POLICY_VIOLATION` (returns `PolicyViolationDetails` with an
exemption key where the policy is exemptible) · `TOO_MANY_MUTATE_OPERATIONS` ·
`RESOURCE_EXHAUSTED`. Full catalog: `errors/google-ads-problem-types.yml`.

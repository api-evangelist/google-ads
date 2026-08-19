---
name: google-ads-upload-offline-conversions
description: >-
  Send offline conversion events, adjustments and customer-match user data back into
  Google Ads. Handles PII, so the consent and hashing rules are part of the skill.
api: Google Ads API
apiId: google-ads:google-ads-api
version: v25
spec: openapi/google-ads-api-v25-openapi.yml
operations:
  - googleads_customers_uploadClickConversions
  - googleads_customers_uploadCallConversions
  - googleads_customers_uploadConversionAdjustments
  - googleads_customers_uploadUserData
  - googleads_customers_offlineUserDataJobs_create
  - googleads_customers_offlineUserDataJobs_addOperations
  - googleads_customers_offlineUserDataJobs_run
consequence: write
handles_pii: true
human_in_the_loop: recommended
generated: '2026-08-13'
method: generated
source: >-
  openapi/google-ads-api-v25-openapi.yml (operationIds verified against the spec),
  conventions/google-ads-conventions.yml, rate-limits/google-ads-rate-limits.yml
---

# Upload offline conversions to Google Ads

Closing the loop between a CRM and Google Ads. Two distinct paths: **conversion uploads**
(an event happened, attribute it to a click) and **customer match** (a list of people,
matched by hashed identifiers).

## Path A — offline conversions

1. **Upload click conversions.** `googleads_customers_uploadClickConversions`
   (`POST /v25/customers/{customersId}:uploadClickConversions`). Each conversion carries a
   `gclid` (or `gbraid`/`wbraid`), the `conversionAction` resource name, a
   `conversionDateTime` and a `conversionValue`. `googleads_customers_uploadCallConversions`
   is the phone-call equivalent, keyed on caller id and call start time.

2. **Correct or retract afterwards.** `googleads_customers_uploadConversionAdjustments`
   restates a value (`RESTATEMENT`) or removes a conversion (`RETRACTION`).

3. **Batch at the documented ceiling.** 2,000 conversions per request — more returns
   `TOO_MANY_CONVERSIONS_IN_REQUEST`.

Set `partialFailure: true` here. Conversion uploads are inherently dirty (stale gclids,
out-of-window timestamps) and you want the good rows to land while the bad ones come back
indexed in the `partial_failure_error`.

## Path B — customer match audiences

1. **Create the job.** `googleads_customers_offlineUserDataJobs_create` with a job type of
   `CUSTOMER_MATCH_USER_LIST` and the target user list.
2. **Add operations.** `googleads_customers_offlineUserDataJobs_addOperations`, in
   batches. Each operation creates or removes a user identified by hashed email, hashed
   phone, or hashed name+address.
3. **Run it.** `googleads_customers_offlineUserDataJobs_run` — asynchronous. It returns a
   long-running operation; poll it with `googleads_customers_operations_get`.

`googleads_customers_uploadUserData` is the synchronous alternative for smaller,
non-customer-match user data uploads.

## PII rules — non-negotiable

- **Hash before you send.** Email addresses and phone numbers must be normalised then
  SHA-256 hashed. Normalise first: lowercase and trim email, strip Gmail dots where
  applicable, convert phone numbers to E.164. Hashing an un-normalised value produces a
  hash that matches nothing.
- **Do not log the plaintext.** An agent running this skill should never write raw
  identifiers to a transcript, a scratch file or an error message.
- **Consent is a precondition, not a field.** Google requires that the advertiser has the
  necessary consent and disclosure to upload this data. Confirm it before the first call;
  the API will not check it for you.
- **Conversion timestamps need a timezone offset** and must fall inside the conversion
  action's click-through window, or the row is rejected.

## Rules that will bite you

- **No idempotency key.** Re-uploading the same conversion double-counts it. Track what
  you have already sent on your side, keyed on gclid + conversionDateTime.
- **Every operation counts against the daily quota**, so a 2,000-row upload consumes 2,000
  operations — most of an Explorer-access day.
- **Attribution is asynchronous.** A successful upload does not mean the conversion is
  attributed; matching and attribution happen later and may still drop the row.

## Errors worth handling

`TOO_MANY_CONVERSIONS_IN_REQUEST` · `PARTIAL_FAILURE` (read the indexed errors) ·
`RESOURCE_NOT_FOUND` (wrong conversionAction resource name) · `RESOURCE_EXHAUSTED`.
Full catalog: `errors/google-ads-problem-types.yml`.

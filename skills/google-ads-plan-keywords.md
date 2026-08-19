---
name: google-ads-plan-keywords
description: >-
  Research keyword ideas, historical volume and forecast metrics before committing budget.
  Read-only, but rate-limited to 1 request per second per account.
api: Google Ads API
apiId: google-ads:google-ads-api
version: v25
spec: openapi/google-ads-api-v25-openapi.yml
operations:
  - googleads_customers_generateKeywordIdeas
  - googleads_customers_generateKeywordHistoricalMetrics
  - googleads_customers_generateKeywordForecastMetrics
  - googleads_customers_generateReachForecast
  - googleads_listPlannableLocations
  - googleads_listPlannableProducts
consequence: read
generated: '2026-08-13'
method: generated
source: >-
  openapi/google-ads-api-v25-openapi.yml (operationIds verified against the spec),
  rate-limits/google-ads-rate-limits.yml
---

# Plan keywords and forecast reach

The planning surface answers "what should we bid on and what will it cost" without
creating anything. It is the cheapest useful thing an agent can do against a Google Ads
account, and the easiest to rate-limit yourself out of.

## Steps

1. **Resolve targeting constants.** `googleads_listPlannableLocations` and
   `googleads_listPlannableProducts` (`POST /v25:listPlannableLocations`,
   `POST /v25:listPlannableProducts`) return the location and product ids the planning
   operations accept. `googleads_geoTargetConstants_suggest` maps a place name to a geo
   target constant.

2. **Generate ideas.** `googleads_customers_generateKeywordIdeas`
   (`POST /v25/customers/{customersId}:generateKeywordIdeas`) from seed keywords, a URL,
   or both. Returns ideas with average monthly searches and competition.

3. **Get historical volume.** `googleads_customers_generateKeywordHistoricalMetrics` for
   a concrete keyword list — monthly search volume, competition index, and bid range.

4. **Forecast performance.** `googleads_customers_generateKeywordForecastMetrics` takes a
   proposed campaign shape (keywords, bids, budget) and returns projected impressions,
   clicks, cost and conversions. `googleads_customers_generateReachForecast` is the
   video/display equivalent, projecting on-target reach and frequency.

## Rules that will bite you

- **1 QPS.** Planning methods are limited to one request per second per CID, and keyword
  planning methods to one request per second per customer id. Exceeding it returns
  `RESOURCE_EXHAUSTED` — serialise these calls, do not fan them out.
- **Every planning call is still an operation** against the daily quota. At Explorer
  access, an exploratory sweep of a few hundred seed sets will exhaust the day.
- **Forecasts are estimates, not commitments.** They come from Google's models, are
  bounded by the inputs you supply, and will not match what a launched campaign delivers.
  Say so when reporting them.
- **Money is micros** throughout — bids, budgets and forecast costs alike.
- **Nothing here creates a campaign.** Keyword plans (`keywordPlans:mutate` and the
  keywordPlan* resources) are a separate saved-planning surface; the generate* operations
  above are stateless and leave no trace on the account.

## Errors worth handling

`RESOURCE_EXHAUSTED` (back off for `QuotaErrorDetails.retry_delay`; the 1 QPS limit trips
this constantly) · `REQUIRED_FIELD_MISSING` · `KEYWORD_PLAN_IDEA_ERROR` family ·
`REACH_PLAN_ERROR` family. Full catalog: `errors/google-ads-problem-types.yml`.

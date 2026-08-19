---
name: google-ads-report-performance
description: >-
  Pull performance data out of a Google Ads account with GAQL — discover the legal fields
  for a resource first, then stream the report. Read-only.
api: Google Ads API
apiId: google-ads:google-ads-api
version: v25
spec: openapi/google-ads-api-v25-openapi.yml
operations:
  - googleads_customers_listAccessibleCustomers
  - googleads_googleAdsFields_search
  - googleads_customers_googleAds_searchStream
  - googleads_customers_googleAds_search
generated: '2026-08-13'
method: generated
source: >-
  openapi/google-ads-api-v25-openapi.yml (operationIds verified against the spec) plus
  conventions/google-ads-conventions.yml and errors/google-ads-problem-types.yml
---

# Report on Google Ads performance

There is no `GET /campaigns` on this API. Every read is a GAQL query POSTed to a search
operation. Do not guess field names — the legal fields differ per resource and the API
will reject an invalid projection rather than ignore it.

## Before you start

- OAuth 2.0 access token with the single scope `https://www.googleapis.com/auth/adwords`.
- `developer-token` header. Test access can only read test accounts.
- `login-customer-id` header when reaching a client account through a manager account.

## Steps

1. **Find the accounts you can reach.** `googleads_customers_listAccessibleCustomers`
   (`GET /v25/customers:listAccessibleCustomers`). Returns resource names of the form
   `customers/{customer_id}`. Strip the prefix to get the customer id used in every path
   below.

2. **Discover the fields for the resource you want to report on.**
   `googleads_googleAdsFields_search` (`POST /v25/googleAdsFields:search`) with a query
   like:

   ```
   SELECT name, selectable, filterable, sortable
   WHERE name LIKE 'campaign.%' AND category = 'ATTRIBUTE'
   ```

   Run it again without the category filter to pick up the `metrics.*` and `segments.*`
   fields compatible with that resource. Cache the result — the field catalog changes only
   at version boundaries.

3. **Run the report.** `googleads_customers_googleAds_searchStream`
   (`POST /v25/customers/{customersId}/googleAds:searchStream`) with a GAQL query in the
   request body:

   ```
   SELECT campaign.id, campaign.name, campaign.status,
          metrics.impressions, metrics.clicks, metrics.cost_micros
   FROM campaign
   WHERE segments.date DURING LAST_30_DAYS
   ORDER BY metrics.cost_micros DESC
   PARAMETERS omit_unselected_resource_names=true
   ```

   Use `searchStream` for reports — it returns the whole result set in chunks with no
   paging. Use `googleads_customers_googleAds_search` instead when you specifically want
   page-at-a-time behaviour with `pageSize` / `pageToken`; a follow-up page request with a
   valid token does not consume additional quota.

## Rules that will bite you

- **Field names are snake_case inside GAQL** (`metrics.cost_micros`) but lowerCamelCase in
  the JSON response (`costMicros`). The reference docs show the proto form.
- **Money is micros.** `cost_micros` of 1500000 is 1.50 in the account currency. Divide by
  1,000,000; never parse as a float.
- **Quota counts operations, not rows.** One search or searchStream call is one operation
  regardless of result size. At Explorer access that is one of 2,880 per day.
- **Throttling arrives in the body, not the headers.** A `RESOURCE_EXHAUSTED` error carries
  `QuotaErrorDetails` with `rate_scope` (ACCOUNT or DEVELOPER), `rate_name` and
  `retry_delay`. Wait `retry_delay`, then back off exponentially. There is no
  `Retry-After` header to read.
- **Test accounts return empty metrics.** Impressions, clicks and cost are always zero in
  a test account — there is no serving data to report on.

## Errors worth handling

`GOOGLE_ACCOUNT_COOKIE_INVALID` (refresh the token) · `DEVELOPER_TOKEN_NOT_APPROVED`
(the token is Test access and you called a production account) · `USER_PERMISSION_DENIED`
(missing or wrong `login-customer-id`) · `QUERY_ERROR` (invalid GAQL — go back to step 2)
· `RESOURCE_EXHAUSTED` (see above). Full catalog: `errors/google-ads-problem-types.yml`.

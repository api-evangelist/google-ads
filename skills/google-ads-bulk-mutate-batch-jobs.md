---
name: google-ads-bulk-mutate-batch-jobs
description: >-
  Apply changes above the 10,000-operation-per-request ceiling asynchronously with
  BatchJobService, and read the per-operation results back.
api: Google Ads API
apiId: google-ads:google-ads-api
version: v25
spec: openapi/google-ads-api-v25-openapi.yml
operations:
  - googleads_customers_batchJobs_mutate
  - googleads_customers_batchJobs_addOperations
  - googleads_customers_batchJobs_run
  - googleads_customers_batchJobs_listResults
  - googleads_customers_operations_get
consequence: write
human_in_the_loop: required
generated: '2026-08-13'
method: generated
source: >-
  openapi/google-ads-api-v25-openapi.yml (operationIds verified against the spec),
  conventions/google-ads-conventions.yml, rate-limits/google-ads-rate-limits.yml
---

# Bulk-mutate a Google Ads account with batch jobs

A synchronous mutate tops out at 10,000 operations. Anything larger — a full account
restructure, a keyword migration, a bulk pause — goes through BatchJobService, which is
asynchronous and returns results per operation.

**This changes live advertising.** Get a human decision on the operation set before
running the job. There is no idempotency key and no rollback.

## Steps

1. **Create the job.** `googleads_customers_batchJobs_mutate`
   (`POST /v25/customers/{customersId}/batchJobs:mutate`) with a create operation. Returns
   the batch job resource name.

2. **Add operations.** `googleads_customers_batchJobs_addOperations`
   (`POST /v25/customers/{customersId}/batchJobs/{batchJobsId}:addOperations`), repeatedly.
   Each call carries a page of mutate operations of any resource type — the same
   `mutateOperations` shape `googleAds:mutate` takes, so temp ids work across the whole
   job. Keep the `sequenceToken` from each response and pass it to the next call, or
   operations will be dropped.

3. **Run it.** `googleads_customers_batchJobs_run`
   (`POST /v25/customers/{customersId}/batchJobs/{batchJobsId}:run`). Returns a
   `google.longrunning.Operation`.

4. **Poll for completion.** `googleads_customers_operations_get`
   (`GET /v25/customers/{customersId}/operations/{operationsId}`) until done. Poll with
   backoff — every poll is an operation against the daily quota.

5. **Read the results.** `googleads_customers_batchJobs_listResults`
   (`GET /v25/customers/{customersId}/batchJobs/{batchJobsId}:listResults`). Each row is
   the outcome of one input operation, in order, with either the mutated resource or a
   `GoogleAdsFailure`. **This is the step people skip.** A job that completes is not a job
   that succeeded — individual operations fail independently and only listResults tells
   you which.

## Rules that will bite you

- **Partial application is the default behaviour.** A batch job is not a transaction.
  Some operations land and some do not. Plan for a mixed outcome and reconcile from
  listResults.
- **Sequence tokens are mandatory** across addOperations calls. Losing one silently
  truncates the job.
- **Every operation counts** against the daily quota — a 100,000-operation job needs
  Standard access, which is unlimited; Basic access (15,000/day) cannot run it in a day.
- **Validate first.** There is no `validateOnly` on a batch job. Dry-run a representative
  slice through `googleads_customers_googleAds_mutate` with `validateOnly: true` before
  building the job.
- **Do not retry a run.** Re-running a job or resubmitting the same operations after a
  timeout duplicates the changes. Poll the long-running operation instead.

## Errors worth handling

`BATCH_JOB_ERROR` family (including CANNOT_MODIFY_JOB_AFTER_JOB_STARTS_RUNNING and
INVALID_SEQUENCE_TOKEN) · per-operation `GoogleAdsFailure` rows in listResults ·
`RESOURCE_EXHAUSTED`. Full catalog: `errors/google-ads-problem-types.yml`.

---
name: acceldata-create-and-run-data-quality-policy
description: Create a Data Quality policy against an ADOC catalog asset, run it, and read the result — including the concurrency and reversibility rules that decide whether a retry is safe.
api: acceldata:acceldata-catalog-api
generated: '2026-08-29'
method: generated
source: openapi/_original/acceldata-catalog-api-openapi.json
operations:
  - listAssetTypes
  - getAssetMetadata
  - createDataQualityRule
  - getDataQualityRule
  - setRuleSchedule
  - triggerDataQualityExecution
  - getDataQualityExecutions
  - getDataQualityExecutionDetail
  - getDataQualityExecutionResult
  - unarchiveDataQualityRule
---

# Create and run a Data Quality policy

Every operationId below is grepped from Acceldata's own published Catalog API contract
(`openapi/_original/acceldata-catalog-api-openapi.json`). Nothing here is invented.

## Before you start

- **Host.** There is no shared Acceldata API host. The base is `https://{adoc-host}` — your
  own ADOC control plane, given to you by an administrator. Paths in this skill already
  include the `/catalog-server/api` prefix.
- **Credentials.** Send `accessKey` and `secretKey` as two separate headers on every call,
  plus `accept: application/json` (and `content-type: application/json` when there is a body).
  Generate the pair in the ADOC UI at Control Center > Security > API Keys. The secret is
  shown once.
- **Permissions.** This flow needs `ASSET_VIEW`, `POLICY_VIEW`, `POLICY_CREATE`,
  `POLICY_MODIFY` and `POLICY_EXECUTE`. A missing permission returns 403 — and so does a
  missing asset, so treat 403 as ambiguous.

## Steps

1. **Confirm the asset exists.** `getAssetMetadata`
   `GET /catalog-server/api/assets/{id}/metadata`. Requires `ASSET_VIEW` and
   `ASSET_METADATA_VIEW`. Use `listAssetTypes` (`GET /catalog-server/api/asset-types`) first
   if you need to know what kind of thing you are pointing at.

2. **Create the policy.** `createDataQualityRule`
   `POST /catalog-server/api/rules/data-quality`. The body carries the rule definition and a
   `backingAsset`. Requires `POLICY_CREATE`.

   > **There is no idempotency key.** If this call times out, do NOT blind-retry — you will
   > create a duplicate policy. Recover with `listDataQualityRules`
   > (`GET /catalog-server/api/rules/data-quality`) or `getDataQualityRule` by name
   > (`GET /catalog-server/api/rules/data-quality/{identifier}`), which accepts an id or a name.

3. **Schedule it, if it should run unattended.** `setRuleSchedule`
   `PUT /catalog-server/api/rules/{id}/schedule`. Since 26.8.0 a policy accepts up to seven
   independent cron expressions via `jobSchedule.cronExpressions`, sharing one timezone.
   A 422 here means "cron not configured, schedule state conflict, or wrong rule type".

4. **Run it.** `triggerDataQualityExecution`
   `POST /catalog-server/api/rules/data-quality/{id}/executions`, or by name with
   `triggerDataQualityExecutionByName`. Requires `POLICY_EXECUTE`.

   > **422 is expected, not an error to escalate.** The contract returns
   > `Previous execution of rule '{name}' has not completed. Not running the rule.`
   > This is per-rule single-flight. Back off and re-trigger; do not treat it as a failure
   > of the policy.

5. **Poll for the outcome.** `getDataQualityExecutions`
   `GET /catalog-server/api/rules/data-quality/{id}/executions` lists runs. Then
   `getDataQualityExecutionDetail` `GET /catalog-server/api/rules/data-quality/executions/{id}`
   and `getDataQualityExecutionResult`
   `GET /catalog-server/api/rules/data-quality/executions/{id}/result` for the per-item
   outcome. Pagination is `page` / `size` / `sortBy` on this API.

## If you need to undo

`deleteDataQualityRule` `DELETE /catalog-server/api/rules/data-quality/{id}` is described in
the contract as **"Delete (archive)"**, and it is reversible: `unarchiveDataQualityRule`
`POST /catalog-server/api/rules/data-quality/{id}/unarchive` restores it.

**No retention window is published.** Acceldata does not state how long an archived policy
stays restorable, so treat recovery as best-effort and unarchive promptly.

ADOC also archives a policy **automatically** when a column the policy references is deleted
or renamed. Archived policies cannot execute. If a policy silently stops producing results,
check for that before rebuilding it — unarchive is the fix, not re-creation.

## Errors you will actually see

| Code | Meaning here | Retry? |
| --- | --- | --- |
| 400 | Missing or non-numeric `id`, or rule validation failure | No — fix the input |
| 403 | Missing permission **or** asset not present | No — the two are indistinguishable |
| 404 | `Rule with the given name: {name} not found` | No |
| 422 | Execution already running, schedule conflict, or wrong rule type | Yes for the execution case, after a delay |
| 500 | Server-side failure | Yes, with backoff |

Errors do **not** use RFC 9457 problem+json. See `errors/acceldata-problem-types.yml` — three
different envelopes are in circulation.

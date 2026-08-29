# Written by API Evangelist, not harvested from the provider

These documents were in `openapi/_original/`, which is the verbatim record of what the PROVIDER
published. They are not that. Each carries an explicit authorship marker — `x-derived-from`,
`x-generated-from: documentation`, or an AE-authored `x-method` — saying we built it.

The Kin Score credits the presence of `_original/` as evidence the provider published a contract,
and grades a marked document as `derived` separately. Leaving these where they were meant the same
file was discounted once and credited once.

Moved, not deleted: they describe real APIs and the pipeline reads them. The only thing wrong was
the claim their location made about who wrote them.

Moved 2026-08-29, roadmap#2 item 4 / roadmap#48.

---

## Superseded 2026-08-29 by the provider's own contracts

Acceldata DOES publish machine-readable OpenAPI. It is served by a Scalar-backed API
reference at `documentation.acceldata.io`, which loads each spec from
`/docs/acceldata/specs/<slug>/openapi.json` — a path the docs site never links directly, so
earlier rounds concluded "no spec" and authored these documents from prose instead.

Now captured verbatim in `openapi/_original/`:

| slug | title | OpenAPI | operations |
| --- | --- | --- | --- |
| `catalog` | Catalog API | 3.1.1 | 104 |
| `administration` | Admin API | 3.1.1 | 31 |
| `tags` | Tag Services | 3.0.3 | 5 |

The documents in this directory describe a surface that does not match the real one. Their
base URL, `https://api.acceldata.app/v1`, appears in no Acceldata documentation: the
published base is the customer's own ADOC host, `https://<HOST>/catalog-server/api/...`
(https://docs.acceldata.io/api/authentication), and their auth header, `X-API-Key`, is not
what the API takes either — it takes an `accessKey` + `secretKey` pair. Their operationIds
(`listAlerts`, `listDatasets`) exist in no published contract.

Everything downstream of them in this repo — `arazzo/`, `collections/`, `examples/`,
`json-schema/`, `json-structure/`, `agentic-access/`, `postman/` and the seven `apis[]`
entries whose `baseURL` is `api.acceldata.app/v1` — inherits that provenance and should be
regenerated from `openapi/_original/` on the next refine pass.

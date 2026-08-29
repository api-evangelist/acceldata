---
name: acceldata-discover-and-tag-assets
description: Find an ADOC catalog asset, read its metadata and lineage, and apply governed tags and labels to it — the discovery half of the Acceldata Catalog API.
api: acceldata:acceldata-catalog-api
generated: '2026-08-29'
method: generated
source: openapi/_original/acceldata-catalog-api-openapi.json, openapi/_original/acceldata-tags-api-openapi.json
operations:
  - listAssetTypes
  - getAssetMetadata
  - getAssetTagsById
  - addAssetTag
  - deleteAssetTag
  - getAssetLabels
  - updateAssetLabels
  - watchAsset
  - unwatchAsset
  - getAssetActivity
  - PublicTagService_CreateTag
---

# Discover and tag catalog assets

## Addressing an asset

Assets carry **two** identifiers and the contract accepts both: a numeric `id` and a string
`uid`. Watch operations publish an explicit by-uid variant (`watchAssetByUid`,
`unwatchAssetByUid`). There are no typed id prefixes, so an id on its own tells you nothing
about what it points at — call `listAssetTypes`
(`GET /catalog-server/api/asset-types`) if you need the type.

## Steps

1. **Read what the asset is.** `getAssetMetadata`
   `GET /catalog-server/api/assets/{id}/metadata` — requires `ASSET_VIEW` **and**
   `ASSET_METADATA_VIEW`. Returns `StandardResponse<MetaData>`.

2. **Sample it, asynchronously.** `requestAssetSampleAsync`
   `POST /catalog-server/api/assets/{id}/sample/async` returns a `requestId`; collect the
   result with `getAssetSampleResult`
   `GET /catalog-server/api/assets/sample/result/{requestId}`. This is a two-call pattern —
   do not expect data on the first response.

3. **Read existing tags and labels.** `getAssetTagsById`
   `GET /catalog-server/api/assets/{id}/tags` and `getAssetLabels`
   `GET /catalog-server/api/assets/{id}/labels`. Requires `TAGS_VIEW`.

4. **Apply a tag.** `addAssetTag` `POST /catalog-server/api/assets/{id}/tag`. Requires
   `ASSET_VIEW` and `TAGS_MODIFY`.

   Since release 26.8.0, tags and labels are one **unified** key-value model managed from a
   central library. If the key you want does not exist yet, create it first with
   `PublicTagService_CreateTag` `POST /api/tags/v1` on the Tag Services surface (note the
   different path prefix and the `TAGS_CREATE` permission). Keys are typed `GOVERNED` or
   `USER`.

5. **Set labels.** `updateAssetLabels` `PUT /catalog-server/api/assets/{id}/labels` — this is
   a **PUT**, so it replaces the label set rather than appending. Read with `getAssetLabels`
   first and merge client-side.

6. **Subscribe to changes.** `watchAsset` `POST /catalog-server/api/assets/{id}/watch`;
   reverse with `unwatchAsset` `DELETE /catalog-server/api/assets/{id}/watch`.

7. **Read the activity trail.** `getAssetActivity`
   `GET /catalog-server/api/assets/{id}/activity` and `getAssetComments`
   `GET /catalog-server/api/assets/{id}/comments`.

## Reversibility

- `deleteAssetTag` `DELETE /catalog-server/api/assets/{id}/tag/{tagId}` detaches a tag and is
  fully reversible with `addAssetTag`. Low blast radius.
- `unwatchAsset` is reversible with `watchAsset`.
- `updateAssetLabels` is **destructive by shape** — a PUT with a short list silently drops
  every label you omitted, and there is no undo. Always read-merge-write.

## Pagination and errors

Catalog list operations page with `page`, `size` and `sortBy`, and wrap results in a `meta`
object. Note that the Administration API uses `first`/`max` instead, and the published docs
guidance refers to `limit`/`offset` — three vocabularies for one product. Do not carry
parameters across surfaces.

403 on a catalog read means either "no permission" or "asset does not exist"; the contract
says so explicitly and does not distinguish them.

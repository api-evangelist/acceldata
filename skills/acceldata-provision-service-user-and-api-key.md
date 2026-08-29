---
name: acceldata-provision-service-user-and-api-key
description: Create a machine identity in ADOC, assign it roles, and issue and revoke its API key pair — including what SCIM-managed identities will refuse.
api: acceldata:acceldata-administration-api
generated: '2026-08-29'
method: generated
source: openapi/_original/acceldata-administration-api-openapi.json
operations:
  - createServiceUser
  - listServiceUsers
  - getServiceUser
  - addServiceUserRoles
  - removeServiceUserRoles
  - createServiceUserApiKey
  - deleteServiceUserApiKey
  - getGroupAvailableRoles
  - listUsers
  - assignUserGroups
---

# Provision a service user and issue its API key

This is the flow to run **once**, by a human or a privileged automation, before any agent can
call the Acceldata APIs at all.

## Before you start

- Base is `https://{adoc-host}/admin/api` — note that the Administration API uses a different
  path prefix from the Catalog API (`/catalog-server/api`) and a different pagination style.
- Permissions: `CREATE_SERVICE_USERS`, `MODIFY_SERVICE_USERS`, `VIEW_ROLE`,
  `MODIFY_API_KEYS`.

## Steps

1. **Create the machine identity.** `createServiceUser`
   `POST /admin/api/v1/service-users`. Requires `CREATE_SERVICE_USERS`. Use a service user,
   not a human account — an API key issued against a person dies with their offboarding.

2. **Find the roles to grant.** `getGroupAvailableRoles`
   `GET /admin/api/groups/{groupId}/available-roles` lists what can be assigned. Roles are
   typed `FEATURE_ROLE` or `RESOURCE_ROLE`, matching ADOC's tenant-role and domain-role
   split.

3. **Assign least privilege.** `addServiceUserRoles`
   `PUT /admin/api/v1/service-users/{serviceUserId}/add-roles`. Grant only the permissions the
   integration needs — `ASSET_VIEW` for a reader, plus `POLICY_EXECUTE` for a scheduler, and
   so on. See `scopes/acceldata-scopes.yml` for the full permission list with the operation
   count behind each one.

4. **Issue the key pair.** `createServiceUserApiKey`
   `POST /admin/api/v1/service-users/{serviceUserId}/api-key`. Requires `MODIFY_API_KEYS`.

   > **The secret is shown once.** Capture `secretKey` from this response and store it
   > immediately. There is no read-back operation and no restore. Keys also carry an
   > operator-set validity date and stop working when it passes.

5. **Verify.** `listServiceUsers` `GET /admin/api/v1/service-users/list` and
   `getUserApiKeys` `GET /admin/api/users/{userId}/api-keys` confirm what exists.
   Pagination here is `first` / `max`, defaulting to `first=0`, `max=10`.

## Revocation

`deleteServiceUserApiKey`
`DELETE /admin/api/v1/service-users/{serviceUserId}/api-key/{accessKey}` — note the key is
addressed by its **accessKey**, the public half. `deleteApiKey`
`DELETE /admin/api/users/api-keys/{accessKey}` does the same for a user-owned key.

**Irreversible.** There is no restore operation for a deleted key, and the secret cannot be
re-read. Rotation means issue-new-then-delete-old, in that order.

## SCIM-managed identities will refuse you

If your tenant provisions identity over SCIM from Okta, Entra or another IdP, the
Administration API is read-mostly for those objects. The contract returns 403 with:

- `Cannot modify SCIM-managed user or group assignments` — on `updateUser`,
  `assignUserGroups`, `removeUserGroups`
- `Cannot rename SCIM-managed groups` — on `updateGroup`
- `Cannot delete SCIM-managed groups` — on `deleteGroup`
- `Cannot modify SCIM-managed user` — on `removeUser`

Check the `scimManaged` boolean, which is a **required** field on both `User` and `Group`,
before attempting any write. You can also filter groups with the `scimEnabled` query
parameter. The correct fix for a 403 of this kind is to make the change upstream in the
identity provider, not to retry.

## Errors

`Status` responses on this API are `{ message: string, status: boolean }` — a different
envelope from the Tag Services `google.rpc.Status` shape. 500s here read `Failed to update
user`, `Failed to remove user`, `Failed to assign groups`; retry with backoff. There is no
idempotency key, so a retried `createServiceUser` can create a duplicate identity — list
before you retry.

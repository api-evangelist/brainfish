---
name: Sync an API catalog into Brainfish
description: Create a catalog and sync content (e.g. an OpenAPI spec) so a Brainfish agent can answer from live API knowledge.
api: openapi/brainfish-public-api-openapi-original.json
operations: [validateToken, createCatalog, syncCatalogContent, getCatalog, listCatalogs]
---

# Sync an API catalog into Brainfish

Feed structured API/content into Brainfish so agents answer from up-to-date sources.

## Auth
`Authorization: Bearer bf_api_...` on every request.

## Steps
1. `validateToken` (POST /v1/auth/validate) — confirm the token.
2. `createCatalog` (POST /v1/catalogs) — create a catalog to hold synced content.
3. `syncCatalogContent` (POST /v1/catalogs/{id}/content) — push/sync content (e.g. an OpenAPI
   spec) into the catalog. Re-run on a pipeline to keep it current.
4. `getCatalog` (GET /v1/catalogs/{id}) — read catalog status and item count.
5. `listCatalogs` (GET /v1/catalogs) — enumerate catalogs.

## Conventions
- Rate limit: 25 requests/minute; honor `X-RateLimit-Reset` on `429`.
- Errors return `{ error, message, details, timestamp, requestId }`.
- No idempotency key — guard against duplicate catalog creation yourself.

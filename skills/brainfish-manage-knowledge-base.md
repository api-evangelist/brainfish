---
name: Manage a Brainfish knowledge base
description: Create a collection, add and organize documents, and search the knowledge base via the Brainfish Public API.
api: openapi/brainfish-public-api-openapi-original.json
operations: [validateToken, createCollection, createDocument, updateDocument, moveDocument, searchDocuments]
---

# Manage a Brainfish knowledge base

Use the Brainfish Public API (`https://api.brainfi.sh`) to build and maintain a knowledge base.

## Auth
Send `Authorization: Bearer bf_api_...` on every request (HTTPS only). Create tokens in the
dashboard under Settings → API Tokens. The legacy `access-token` header is deprecated — use Bearer.

## Steps
1. `validateToken` (POST /v1/auth/validate) — confirm the token and read the user/team it belongs to.
2. `createCollection` (POST /v1/collections) — create a collection to group articles.
3. `createDocument` (POST /v1/documents) — add a document to the collection (`collectionId`).
4. `updateDocument` (PUT /v1/documents/{id}) — edit title, content, or publish status.
5. `moveDocument` (POST /v1/documents/{id}/move) — relocate a document to another collection.
6. `searchDocuments` (POST /v1/documents/search) — semantic search to verify coverage.

## Conventions
- Pagination on list endpoints is `limit`/`offset` with `sort` + `direction`.
- Rate limit: 25 requests/minute. On `429`, honor `X-RateLimit-Reset` (Unix timestamp) before retrying.
- Errors return `{ error, message, details, timestamp, requestId }` — log `requestId` for support.
- No idempotency key is supported; do not assume safe automatic retries on writes.

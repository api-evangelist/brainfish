---
name: Generate an AI answer with Brainfish
description: Generate a grounded, cited AI answer to an end-user question and follow-up questions via the Brainfish Public API.
api: openapi/brainfish-public-api-openapi-original.json
operations: [generateUserAnswer, generateAnswer, generateFollowUpQuestions]
---

# Generate an AI answer with Brainfish

Answer end-user questions grounded in the knowledge base, with source citations.

## Auth
`Authorization: Bearer bf_api_...`. Answer generation additionally requires an `agent-key`
header identifying which agent/widget to use (find it in the dashboard under Agents).

## Steps
1. `generateUserAnswer` (POST /v1/users/answer) — generate an AI answer with source citations
   for an end-user question. (Internal/agent variant: `generateAnswer`, POST /v1/agents/answer.)
2. `generateFollowUpQuestions` (POST /v1/conversations/{conversationId}/follow-ups) — generate
   suggested follow-up questions for the conversation.

## Conventions
- Answer endpoints can stream via `text/event-stream` (SSE) — handle `start`/`progress`/`content`/`end` events.
- Rate limit: 25 requests/minute; back off on `429` using `X-RateLimit-Reset`.
- Errors return `{ error, message, details, timestamp, requestId }`.

---
type: component
created: 2026-10-20
layer: backend
status: implemented
path: backend/src/middlewares/auth.middleware.ts
tags: [component, backend, security]
related: [Auth Module]
depends_on: [Prisma Data Layer]
decided_by: [ADR-002 JWT Access and Refresh Tokens, ADR-012 JWT Access Token with Opaque Rotating Refresh Token]
sources: ["practical work 4: typed ontology relations", "practical work 5: record-adr ADR-012"]
---
# Auth Middleware

## Responsibility
Verifies the access token from the `Authorization: Bearer …` header and attaches the user id to `req` (type extended in `backend/src/types/express.d.ts`). Protects all routes except `register / login / refresh` of [[Auth Module]].

## Used by
[[Goal Module]] · [[Task Module]] · [[AI Module]] · [[User Module]]

## Relations
- depends_on → [[Prisma Data Layer]]
- decided_by → [[ADR-002 JWT Access and Refresh Tokens]]
- decided_by → [[ADR-012 JWT Access Token with Opaque Rotating Refresh Token]]

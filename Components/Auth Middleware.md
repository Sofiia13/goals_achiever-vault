---
type: component
created: 2026-10-20
layer: backend
status: implemented
path: backend/src/middlewares/auth.middleware.ts
tags: [component, backend, security]
related: [Auth Module]
---
# Auth Middleware

## Responsibility
Verifies the access token from the `Authorization: Bearer …` header and attaches the user id to `req` (type extended in `backend/src/types/express.d.ts`). Protects all routes except `register / login / refresh` of [[Auth Module]].

## Used by
[[Goal Module]] · [[Task Module]] · [[AI Module]] · [[User Module]]

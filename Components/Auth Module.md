---
type: component
created: 2026-10-20
layer: backend
status: implemented
path: backend/src/modules/auth/
tags: [component, backend, security]
related: [Auth Middleware, User Module, ADR-002 JWT Access and Refresh Tokens]
---
# Auth Module

## Responsibility
Registration, login, token refresh and fetching the current user.

## API (`/auth`)
| Method | Path | Auth |
|---|---|---|
| POST | `/register` | — |
| POST | `/login` | — |
| POST | `/refresh` | — |
| GET | `/me` | yes |

## Structure
`auth.routes → auth.controller → auth.service`; validation — `auth.validation.ts`; hashing — `utils/hash.utils.ts` (bcryptjs); tokens — `utils/jwt.utils.ts`. Token scheme — [[ADR-002 JWT Access and Refresh Tokens]].

## Dependencies
[[Prisma Data Layer]] (`User` model, `refreshToken` field).

## Related
[[Auth Middleware]] · [[Auth Context]]

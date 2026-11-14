---
type: decision
created: 2026-10-20
status: superseded
tags: [decision, adr, security]
related: [Auth Module, Auth Middleware, Auth Context]
sources: ["practical work 5: superseded by ADR-012"]
---
# ADR-002 JWT Access and Refresh Tokens

## Context
Frontend (Vercel) and backend are deployed separately; stateless authentication is needed.

## Decision
Short-lived access token + long-lived refresh token (JWT). The refresh token is stored in `User.refreshToken`; passwords are hashed with bcryptjs. Implemented in [[Auth Module]], verified by [[Auth Middleware]].

## Alternatives considered
- Server-side sessions — need a session store and are harder cross-origin;
- third-party provider (Auth0, Clerk) — unnecessary dependency for a course project.

## Consequences
A session can be revoked by clearing `refreshToken`. The client ([[Frontend API Layer]]) should refresh the token on 401 — not yet implemented in the interceptor.

Superseded by [[ADR-012 JWT Access Token with Opaque Rotating Refresh Token]]: the refresh token was never a JWT. Since commit `04ce494` it is an opaque rotating UUID.

---
type: decision
created: 2026-11-14
status: accepted
tags: [decision, adr, backend, security]
related: [ADR-006 CORS Allowlist with Origin Patterns, ADR-011 Backend Unit Tests with Node Test Runner and Module Mocks, Frontend API Layer]
supersedes: [ADR-002 JWT Access and Refresh Tokens]
sources: ["commit 04ce494 (2025-12-15); migration 20251212142824_add_refresh_token; found by unit-tests skill, commit cf1553e; practical work 5"]
---
# ADR-012 JWT Access Token with Opaque Rotating Refresh Token

## Context
[[ADR-002 JWT Access and Refresh Tokens]] states "short-lived access token + long-lived refresh token (JWT)". The code never worked that way. Since commit `04ce494` (2025-12-15, "add registration") `backend/src/utils/jwt.utils.ts` issues the refresh token with `crypto.randomUUID()`, an opaque random string, not a JWT. The unit tests from practical work #5 (`backend/test/utils/jwt.utils.test.ts`, commit `cf1553e`) assert this behaviour and exposed the mismatch. An ADR whose Decision section contradicts the code misleads the agent, so the decision is recorded again as it is actually implemented.

## Decision
- **Access token:** JWT (HS256) signed with `JWT_SECRET`, payload `{ userId, email }`, lifetime `JWT_ACCESS_EXPIRATION` (default `15m`). Sent as `Authorization: Bearer …` and checked by [[Auth Middleware]] (`verifyAccessToken`: `Access token expired` / `Invalid access token`).
- **Refresh token:** opaque UUID v4 from `generateRefreshToken()`, stored in `User.refreshToken` (column added by migration `20251212142824_add_refresh_token`). One active refresh token per user.
- **Rotation:** `POST /auth/refresh` finds the user by `refreshToken` (`prisma.user.findFirst`), issues a new pair and overwrites the stored token, so every refresh token is single-use. Login also overwrites it, which logs out the previous session.
- Passwords are hashed with bcryptjs (10 salt rounds), as in ADR-002.

## Alternatives considered
- Refresh token as a JWT (what ADR-002 described): rejected in practice, because a signed refresh token still has to be stored to be revocable, so the signature adds nothing over a random value.
- Server-side sessions and third-party providers: rejected for the reasons already given in ADR-002 (session store, cross-origin, extra dependency).

## Consequences
- Revocation = set `User.refreshToken` to `null`; rotation also makes stolen-and-used refresh tokens detectable (the legitimate client's next refresh fails).
- The refresh token **has no expiry**: it is valid until the next login or refresh. A time limit would need a new column (`refreshTokenExpiresAt`, W2) and is a follow-up.
- The refresh token is stored **in plain text**; a DB leak exposes live sessions. Storing a hash (like passwords) is a follow-up.
- `jwt.utils.ts:5` falls back to a hardcoded secret if `JWT_SECRET` is missing, so the access tokens become forgeable. This is pinned by a `todo` test (see [[ADR-011 Backend Unit Tests with Node Test Runner and Module Mocks]]). The fix is to fail at startup instead.
- The client ([[Frontend API Layer]]) still does not refresh on 401, as noted in ADR-002.
- ADR-002 gets status `superseded` and is kept as history (guardrail B3).

## Relations
- supersedes → [[ADR-002 JWT Access and Refresh Tokens]]

## Related
- [[ADR-006 CORS Allowlist with Origin Patterns]]

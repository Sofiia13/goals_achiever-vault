---
type: decision
created: 2026-11-14
status: accepted
tags: [decision, adr, backend, deploy, security]
related: [Auth Module, Frontend API Layer, ADR-002 JWT Access and Refresh Tokens]
sources: [commit 2e2cafe (fix CORS)]
---
# ADR-006 CORS Allowlist with Origin Patterns

## Context
The frontend is deployed on Vercel, and every preview deployment gets its own `*.vercel.app` origin. The backend (`backend/src/app.ts`) allowed only an exact list of origins from env, so requests from preview URLs failed with CORS errors. Auth cookies are sent with `credentials: true` ([[ADR-002 JWT Access and Refresh Tokens]]), so `origin: *` is not an option.

## Decision
Two ways to allow an origin in the `cors` callback:
1. the exact list from env (normalized origins), as before;
2. regex patterns: the default `^https://.*\.vercel\.app$` plus extra patterns from `FRONTEND_URL_PATTERNS` (comma-separated).
Requests without an `Origin` header (curl, server-to-server) are allowed. A blocked origin is logged (`CORS blocked for origin: ...`) and rejected.

## Alternatives considered
- `origin: *`: does not work with credentials and is unsafe.
- Adding each preview URL to env by hand: does not scale.

## Consequences
- Preview and production frontends work without changing env.
- The default pattern allows **any** `*.vercel.app` site, including other people's projects. Narrow it to the project's prefix (e.g. `^https://goals-achiever.*\.vercel\.app$`) through `FRONTEND_URL_PATTERNS` or in code.
- New allowed domains are configured through env, without redeploying the code.

## Related
- [[Auth Module]]
- [[Frontend API Layer]]

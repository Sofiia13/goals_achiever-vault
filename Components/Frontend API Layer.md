---
type: component
created: 2026-10-20
layer: frontend
status: implemented
path: frontend/src/shared/api/
tags: [component, frontend]
related: [Auth Context, Auth Module, Goal Module, Task Module, AI Module, User Module]
---
# Frontend API Layer

## Responsibility
Axios wrappers around the backend REST API.

## Files
- `axios.ts` — instance with base URL (`VITE_API_URL`, default `http://localhost:3001`) and a request interceptor that adds the access token from `localStorage`;
- `auth.api.ts` → [[Auth Module]];
- `goals.api.ts` → [[Goal Module]];
- `tasks.api.ts` → [[Task Module]];
- `ai.api.ts` → [[AI Module]];
- `user.api.ts` → [[User Module]].

Response types — `frontend/src/shared/types/api.types.ts`.

## TODO
Automatic token refresh on 401 (calling `/auth/refresh`) is not implemented in the interceptor yet.

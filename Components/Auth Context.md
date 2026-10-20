---
type: component
created: 2026-10-20
layer: frontend
status: implemented
path: frontend/src/shared/context/AuthContext.tsx
tags: [component, frontend, security]
related: [Auth Module, Frontend API Layer]
---
# Auth Context

## Responsibility
React context for auth state (`user`, `isAuthChecked`, `setUser`, `logout`, `refreshUser`; redirects to `/login` when unauthenticated). Accessed via the `useAuth` hook (`frontend/src/shared/hooks/useAuth.ts`). Talks to [[Auth Module]] through [[Frontend API Layer]].

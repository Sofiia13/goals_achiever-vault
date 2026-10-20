---
type: component
created: 2026-10-20
layer: backend
status: implemented
path: backend/prisma/schema.prisma
tags: [component, backend, database]
related: [ADR-003 PostgreSQL with Prisma ORM, Goal, Task]
---
# Prisma Data Layer

## Responsibility
DB schema, migrations and the typed client. Decision — [[ADR-003 PostgreSQL with Prisma ORM]].

## Models
- `User` — profile, `refreshToken`, `money` ([[Coins]]), [[Streak]] fields;
- `Goal` — [[Goal]], `currentStationProgress`;
- `Task` — [[Task]] (both [[Station]] and [[Daily Task]]), `onDelete: Cascade`.

## Files
`backend/prisma/schema.prisma`, `backend/prisma/migrations/`, `backend/prisma/seed.ts`; the client is generated into `backend/src/generated/`, the instance is `backend/src/prisma.ts`.

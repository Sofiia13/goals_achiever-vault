---
type: component
created: 2026-10-20
layer: backend
status: implemented
path: backend/prisma/schema.prisma
tags: [component, backend, database]
related: [ADR-003 PostgreSQL with Prisma ORM, Goal, Task]
decided_by: [ADR-003 PostgreSQL with Prisma ORM, ADR-011 Backend Unit Tests with Node Test Runner and Module Mocks]
sources: ["practical work 5: record-adr ADR-011"]
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

## Relations
- decided_by → [[ADR-003 PostgreSQL with Prisma ORM]]
- decided_by → [[ADR-011 Backend Unit Tests with Node Test Runner and Module Mocks]]

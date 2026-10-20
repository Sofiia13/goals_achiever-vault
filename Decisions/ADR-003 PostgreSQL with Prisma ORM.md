---
type: decision
created: 2026-10-20
status: accepted
tags: [decision, adr, database]
related: [Prisma Data Layer]
---
# ADR-003 PostgreSQL with Prisma ORM

## Context
The data is relational: user → goals → tasks. Migrations and TypeScript typing are needed, plus free DB hosting.

## Decision
PostgreSQL (Neon / Supabase / Render) + Prisma ORM. See [[Prisma Data Layer]].

## Alternatives considered
- MongoDB — weaker support for relations and cascades;
- TypeORM / Sequelize — weaker typing and DX than Prisma.

## Consequences
The schema is the single source of truth for models; the client is generated into `backend/src/generated/`.

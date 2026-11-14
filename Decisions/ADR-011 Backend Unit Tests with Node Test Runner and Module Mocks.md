---
type: decision
created: 2026-11-14
status: accepted
tags: [decision, adr, backend, conventions]
related: [ADR-003 PostgreSQL with Prisma ORM, Streak Service, Task Module, Auth Module]
sources: [commit cf1553e; branch feature/pw5-skills; practical work 5]
---
# ADR-011 Backend Unit Tests with Node Test Runner and Module Mocks

## Context
Until practical work #5 the backend had no tests at all: no test runner, no `test` script, only the harness tests in `harness/**` (`node --test`). Every service imports the singleton from `backend/src/prisma.ts`, which throws without `DATABASE_URL` and opens a `pg` pool, so a module cannot even be imported in a test without a database. Guardrails forbid the obvious shortcuts: a test database means `prisma migrate` / `db push` (W2), a new framework (Jest, Vitest) is a dependency change (W3), and reading `.env` for a real `DATABASE_URL` is blocked (B1).

## Decision
- Runner: Node's built-in `node:test` + `node:assert/strict`, TypeScript through `tsx` (already a devDependency). No new packages.
- `npm --prefix backend test` = `TZ=Europe/Kyiv node --import tsx --experimental-test-module-mocks --test "test/**/*.test.ts"`; `npm --prefix backend run test:types` = `tsc -p test/tsconfig.json`.
- Tests live in `backend/test/**`, mirroring `src/` (`src/services/streak` → `test/services/streak.test.ts`).
- The database is never touched: each test file registers `createPrismaMock()` from `backend/test/helpers/prisma-mock.ts` with `mock.module("../../src/prisma.js", { namedExports: { prisma } })` and only then `await import()`s the code under test. Other services ([[Streak Service]], `UserService`) are mocked the same way.
- Time is frozen with `mock.timers` (`Date`); the fixed `TZ=Europe/Kyiv` makes local-day arithmetic and DST cases deterministic.
- A test that exposes a code defect is kept and marked `{ todo: "BUG: <file>:<line> …" }`: it is reported but does not fail the suite. The fix is a separate task.
- The procedure is formalised as the project skill `.claude/skills/unit-tests` (asserts come from vault concept rules, not from the current code).

## Alternatives considered
- Vitest or Jest: rejected, because it is a new dependency (W3) and duplicates what Node 22+ already ships; the harness tests already use `node --test`.
- A real test database (Docker / Neon branch): rejected, because it needs migrations and a `DATABASE_URL` (W2, B1) and makes unit tests slow and network-dependent.
- Refactor services to accept an injected client: rejected for now, because it changes application code just to enable tests; module mocking gives the same isolation without touching `src/`.

## Consequences
- `backend/src/prisma.ts` must keep exactly one named export `prisma`, and services must import it by path (`../../prisma.js`). Renaming it or switching to a default export breaks every test mock; see [[Prisma Data Layer]].
- `mock.module` is still experimental in Node (flag required); `namedExports` is used because `@types/node` 24 does not type the newer `exports` option.
- The first run (commit `cf1553e`) has 40 passing and 4 `todo` tests. They are real defects found by the tests: the DST off-by-one in [[Streak Service]], the hardcoded fallback JWT secret in `utils/jwt.utils.ts` ([[Auth Module]]), and two non-idempotent status transitions in [[Task Module]] (repeated `done` rewards coins again; `pending → pending` subtracts station progress).
- `backend/test/tsconfig.json` overrides `ignoreDeprecations` to `"5.0"`, because the root `backend/tsconfig.json` (commit `be59e01`) sets `"6.0"`, which the locked TypeScript 5.9.3 rejects. The same error breaks `npm --prefix backend run build`.

## Related
- [[ADR-003 PostgreSQL with Prisma ORM]]

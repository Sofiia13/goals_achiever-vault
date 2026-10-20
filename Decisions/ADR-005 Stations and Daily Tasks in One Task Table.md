---
type: decision
created: 2026-10-20
status: accepted
tags: [decision, adr, database]
related: [Task, Station, Daily Task, Prisma Data Layer]
---
# ADR-005 Stations and Daily Tasks in One Task Table

## Context
The plan has two levels: [[Station|stations]] and [[Daily Task|daily tasks]]. Both have a title, description, date and status.

## Decision
A single `Task` table with a `type` field (`daily` — daily task, anything else — station) and a text `station` field.

## Alternatives considered
A separate `Station` model with a `Task.stationId` FK — a cleaner model, but more migrations and queries.

## Consequences
- Simple CRUD and shared status logic in [[Task Module]].
- A task is linked to its station by name (string), not by FK → fragile on rename. Refactoring candidate.

---
type: concept
created: 2026-10-20
tags: [concept, domain]
related: [Goal, Station, Daily Task, Coins, Streak]
---
# Task

## Definition
A unit of work within a [[Goal]]. All tasks are stored in one `Task` table; the role is defined by the `type` field — see [[ADR-005 Stations and Daily Tasks in One Task Table]]:
- [[Station]] — a large plan milestone (`type` ≠ `daily`);
- [[Daily Task]] — a small task for today (`type = "daily"`).

## Statuses
`pending` → `done` (and back). Transition to `done`:
- awards 2 [[Coins]];
- updates the [[Streak]];
- for a [[Daily Task]], adds `progressContribution` to the station progress.
Reverting `done` → `pending` rolls back coins and progress.

## Attributes
`title`, `description`, `dueDate`, `estimatedMinutes`, `station`, `type`, `progressContribution`.

## Implemented in
[[Task Module]] (`task.service.ts → updateTaskStatus`).

---
type: concept
created: 2026-10-20
aliases: [Objective]
tags: [concept, domain]
related: [Station, Task, AI Plan Generation, Roadmap]
---
# Goal

## Definition
A personal goal the user wants to reach by a deadline. The central entity of the app: tasks, progress and most of the gamification are attached to a goal.

## Attributes
- `title` — goal name; `context` — description / desired outcome (passed into the AI prompt);
- `deadline` — required due date;
- `currentStationProgress` — progress (0–100) of the current [[Station]];
- `completedAt` — completion date (null while the goal is active).

## Rules
- A goal belongs to exactly one user; only the owner can access it (see [[Auth Middleware]]).
- After creation, a goal is split into [[Station|stations]] by [[AI Plan Generation]] or manually.
- Deleting a goal cascades to its [[Task|tasks]].

## Implemented in
[[Goal Module]], `Goal` model in [[Prisma Data Layer]].

## Related
[[Roadmap]] · [[Progress Analytics]] · [[Achievement]]

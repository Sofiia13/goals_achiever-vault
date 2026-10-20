---
type: concept
created: 2026-10-20
aliases: [Badge]
tags: [concept, gamification]
related: [Goal, Task, Streak, Coins, Experience Points]
---
# Achievement

## Definition
A badge unlocked when a statistics threshold is reached (e.g. "First step" — 1+ [[Goal]] created; "Task Warrior" — 25+ [[Task|tasks]] completed).

## Rules
- Declared as `{ id, icon, title, subtitle, unlocked }`.
- `unlocked` is computed from `AchievementStats`: `money`, `currentStreak`, `totalGoals`, `completedGoals`, `completedTasks`, `aiTasks`.
- Not stored in the DB — recomputed on every load; a newly unlocked badge is shown by `AchievementNotifier`.

## Implemented in
`frontend/src/shared/utils/achievements.ts`, data via [[Frontend API Layer]].

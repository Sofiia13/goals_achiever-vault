---
type: concept
created: 2026-10-20
tags: [concept, gamification]
related: [Task, Experience Points, Achievement]
---
# Streak

## Definition
The number of consecutive days on which the user completed at least one [[Task]]. A gamification element that encourages daily activity.

## User fields
`currentStreak`, `longestStreak`, `lastActivityDate`.

## Algorithm (when a task becomes `done`)
- `lastActivityDate == null` → streak = 1;
- 0 days since last activity → unchanged;
- 1 day → streak + 1;
- more than 1 day → streak = 1;
- `longestStreak = max(longestStreak, currentStreak)` — never decreases.

## Implemented in
[[Streak Service]], endpoint `GET /user/streak` in [[User Module]].

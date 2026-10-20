---
type: component
created: 2026-10-20
layer: backend
status: implemented
path: backend/src/services/streak/streak.service.ts
tags: [component, backend, gamification]
related: [Streak, Task Module]
---
# Streak Service

## Responsibility
Implements the [[Streak]] algorithm: `updateUserStreak(userId)` recalculates `currentStreak`, `longestStreak`, `lastActivityDate`.

## Called from
[[Task Module]] when a task becomes `done`.

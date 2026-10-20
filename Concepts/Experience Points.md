---
type: concept
created: 2026-10-20
aliases: [XP]
tags: [concept, gamification]
related: [Level, Streak, Coins, Achievement]
---
# Experience Points

## Definition
Aggregate activity score from which the [[Level]] is calculated. Not stored in the DB — computed on the client from statistics.

## Formula
```
XP = completedTasks × 15 + completedGoals × 60 + currentStreak × 10 + coins × 1
```
Inputs: [[Task]], [[Goal]], [[Streak]], [[Coins]].

## Implemented in
`frontend/src/pages/ProfilePage/ProfilePage.tsx` (see [[Progress Analytics]]).

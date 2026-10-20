---
type: concept
created: 2026-10-20
tags: [concept, analytics]
related: [Task, Goal, Streak, Experience Points, Achievement]
---
# Progress Analytics

## Definition
Statistics of completed [[Task|tasks]] and achieved [[Goal|goals]] per day, week and month (functional requirement #7). Includes weekly activity, [[Streak]], [[Experience Points|XP]] and [[Achievement|achievements]].

## Implemented in
`frontend/src/pages/AnalyticsPage`, `ProfilePage`; data via [[Frontend API Layer]].

## Status
partial — some metrics are computed on the client; backend aggregation is planned.

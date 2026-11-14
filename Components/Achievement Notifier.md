---
type: component
created: 2026-11-14
layer: frontend
status: implemented
path: frontend/src/shared/components/ui/AchievementNotifier/AchievementNotifier.tsx
tags: [component, frontend, gamification]
related: [Achievement, Auth Context, Frontend API Layer, Coins, Streak]
sources: [commit ede1369 (add achievements modal)]
---
# Achievement Notifier

## Responsibility
Shows a modal when the user unlocks a new [[Achievement]]. Mounted once in `frontend/src/app/App.tsx`, so it works on every page.

## How it works
- `checkAchievements()` loads `AchievementStats` (`loadAchievementStats()` in `frontend/src/shared/utils/achievements.ts`, data via [[Frontend API Layer]]) and computes unlocked badges with `getAchievements(stats)`.
- Already shown badge ids are stored in `localStorage` under a per-user key (user id from [[Auth Context]]).
- First run after login (`initialize = true`) only records the current badges as seen, so old achievements do not pop up.
- Later runs push only unseen badges into a display queue (deduplicated).
- Re-checks on window events `progressUpdated`, `moneyUpdated` ([[Coins]]), `streakUpdated` ([[Streak]]), dispatched e.g. from `TaskItem.tsx` after a task is completed.

## Public interface (API / exports)
`AchievementNotifier` (React component, no props).

## Dependencies
[[Auth Context]], [[Frontend API Layer]], `shared/utils/achievements.ts`.

## Known issues / TODO
- "Seen" state lives in `localStorage` only: on another device or after clearing storage, the first load re-initializes silently (no duplicate modals, but also no notification for badges unlocked meanwhile).
- Achievements are recomputed on the client; no server-side record.

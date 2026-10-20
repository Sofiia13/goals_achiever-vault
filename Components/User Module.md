---
type: component
created: 2026-10-20
layer: backend
status: implemented
path: backend/src/modules/user/
tags: [component, backend, gamification]
related: [Coins, Streak, Streak Service]
---
# User Module

## Responsibility
Operations on the user's game stats: [[Coins]] balance and [[Streak]].

## API (`/user`, all behind [[Auth Middleware]])
| Method | Path | Description |
|---|---|---|
| GET | `/money` | current balance |
| POST | `/money/add` | add coins |
| POST | `/money/remove` | remove coins |
| GET | `/streak` | `currentStreak`, `longestStreak` |

## Known issues
`/money/add` is callable directly by the client — the balance can be inflated; awarding coins should stay server-side only.

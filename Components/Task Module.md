---
type: component
created: 2026-10-20
layer: backend
status: implemented
path: backend/src/modules/task/
tags: [component, backend]
related: [Task, Station, Daily Task, Streak Service, User Module]
depends_on: [Auth Middleware, Prisma Data Layer, Streak Service, User Module, AI Module]
implements: [Task, Daily Task]
decided_by: [ADR-005 Stations and Daily Tasks in One Task Table]
sources: ["practical work 4: typed ontology relations"]
---
# Task Module

## Responsibility
Managing [[Task|tasks]], status changes and the related gamification side effects.

## API (`/tasks`, all behind [[Auth Middleware]])
| Method | Path | Description |
|---|---|---|
| GET | `/goals/:goalId/` | all tasks of a goal |
| POST | `/goals/:goalId/` | create manually |
| GET | `/goals/:goalId/daily-tasks` | [[Daily Task|daily tasks]] |
| GET | `/goals/:goalId/stations/:stationTitle/progress` | [[Station]] progress |
| PATCH | `/:taskId/status` | change status |
| PATCH | `/:taskId/details` | edit fields |

## Side effects of `updateTaskStatus`
`done` → +2 [[Coins]] (via [[User Module]]), [[Streak]] update (via [[Streak Service]]), station progress increment. Reverting does the opposite.

## Risk
Side effects run as separate queries without a transaction — a failure can desync coins and status.

## Relations
- depends_on → [[Auth Middleware]]
- depends_on → [[Prisma Data Layer]]
- depends_on → [[Streak Service]]
- depends_on → [[User Module]]
- depends_on → [[AI Module]]
- implements → [[Task]]
- implements → [[Daily Task]]
- decided_by → [[ADR-005 Stations and Daily Tasks in One Task Table]]

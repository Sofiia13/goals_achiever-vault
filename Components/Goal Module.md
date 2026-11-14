---
type: component
created: 2026-10-20
layer: backend
status: partial
path: backend/src/modules/goal/
tags: [component, backend]
related: [Goal, Task Module, AI Module]
depends_on: [Auth Middleware, Prisma Data Layer]
implements: [Goal]
sources: ["practical work 4: typed ontology relations"]
---
# Goal Module

## Responsibility
CRUD for the current user's [[Goal|goals]].

## API (`/goals`, all behind [[Auth Middleware]])
| Method | Path | Description |
|---|---|---|
| GET | `/` | user's goals |
| POST | `/` | create a goal |
| GET | `/:id` | goal by id |
| DELETE | `/:id` | delete (cascades to tasks) |
| GET | `/:id/days-till-deadline` | days until deadline |

## TODO
Editing a goal (`PATCH /:id`) — requirement #2, not implemented yet.

## Dependencies
[[Prisma Data Layer]]

## Relations
- depends_on → [[Auth Middleware]]
- depends_on → [[Prisma Data Layer]]
- implements → [[Goal]]

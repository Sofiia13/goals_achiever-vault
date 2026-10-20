---
type: component
created: 2026-10-20
layer: backend
status: implemented
path: backend/src/modules/ai/
tags: [component, backend, ai]
related: [AI Plan Generation, Plan Adaptation, Daily Task, ADR-001 Google Gemini as AI Provider]
---
# AI Module

## Responsibility
Integration with Google Gemini (`@google/genai`, model `gemini-2.5-flash`) for [[AI Plan Generation]] and [[Plan Adaptation]].

## API (`/ai`, all behind [[Auth Middleware]])
| Method | Path | Cost |
|---|---|---|
| POST | `/plan` | 10 [[Coins]] |
| POST | `/daily-tasks` | 1 [[Coins|coin]] |

## Key `AiService` functions
- `generatePlan(userId, goal, deadline, context)` — stations for a goal;
- `getProgressInfo(goalId)` — current station + completed daily tasks;
- `generateDailyTasks(...)` — [[Daily Task|daily tasks]].

## Configuration
`GEMINI_API_KEY` in `backend/.env`.

## Known issues
- Debug logs print the API key prefix to the console — remove them.
- JSON is parsed without schema validation.

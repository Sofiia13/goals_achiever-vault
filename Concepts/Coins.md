---
type: concept
created: 2026-10-20
aliases: [Money, Balance]
tags: [concept, gamification]
related: [Task, AI Plan Generation, Daily Task, Experience Points]
---
# Coins

## Definition
In-app virtual currency (`User.money`). Both a reward for activity and the "fuel" for AI features — this limits the number of requests to the Gemini free tier.

## Economy
| Event | Change |
|---|---|
| Registration | +20 (starting balance) |
| [[Task]] → `done` | +2 |
| [[Task]] `done` → `pending` | −2 |
| [[AI Plan Generation]] | −10 |
| [[Daily Task]] generation | −1 |

## Implemented in
[[User Module]] (`/user/money`, `/money/add`, `/money/remove`), [[Task Module]], [[AI Module]].

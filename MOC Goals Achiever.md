---
type: moc
created: 2026-10-20
aliases: [Index]
tags: [moc]
---
# MOC Goals Achiever

Single entry point to the knowledge base about Goals Achiever — a web app for planning personal goals with AI planning and gamification. Vault rules are in [[README]].

## 1. Domain
### Planning
- [[Goal]] — user's goal
- [[Station]] — plan milestone
- [[Task]] — task (general entity)
- [[Daily Task]] — task for today
- [[Roadmap]] — goal roadmap

### AI
- [[AI Plan Generation]] — splitting a goal into stations
- [[Plan Adaptation]] — adjusting the plan to progress

### Gamification
- [[Coins]] — virtual currency
- [[Streak]] — activity streak
- [[Experience Points]] — XP
- [[Level]] — user level
- [[Achievement]] — badges

### Analytics
- [[Progress Analytics]]

## 2. Components
### Backend (`backend/src/`)
- [[Auth Module]] · [[Auth Middleware]]
- [[User Module]]
- [[Goal Module]]
- [[Task Module]]
- [[AI Module]]
- [[Streak Service]]
- [[Prisma Data Layer]]

### Frontend (`frontend/src/`)
- [[Frontend API Layer]]
- [[Auth Context]]
- [[Roadmap View]]

## 3. Architecture decisions
- [[ADR-001 Google Gemini as AI Provider]]
- [[ADR-002 JWT Access and Refresh Tokens]]
- [[ADR-003 PostgreSQL with Prisma ORM]]
- [[ADR-004 Separate Knowledge Base Repository]]
- [[ADR-005 Stations and Daily Tasks in One Task Table]]

## 4. Glossary
- [[Glossary]]

## Common agent routes
- **New goal / task feature:** [[Goal]] → [[Task]] → [[Task Module]] → [[Prisma Data Layer]]
- **Coin / streak bug:** [[Coins]] → [[Streak]] → [[Task Module]] → [[Streak Service]]
- **AI prompt changes:** [[AI Plan Generation]] → [[AI Module]] → [[ADR-001 Google Gemini as AI Provider]]
- **Authentication:** [[Auth Module]] → [[ADR-002 JWT Access and Refresh Tokens]] → [[Auth Context]]

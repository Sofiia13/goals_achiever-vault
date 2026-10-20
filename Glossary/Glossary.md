---
type: glossary
created: 2026-10-20
tags: [glossary]
---
# Glossary

Shared terminology between the developer and the agent. Domain terms have their own notes in `Concepts/`.

## Domain terms
| Term | Definition | Note |
|---|---|---|
| Goal | Personal goal with a deadline | [[Goal]] |
| Task | Unit of work within a goal | [[Task]] |
| Station | Milestone of a goal plan | [[Station]] |
| Daily Task | Small task for today, `type = daily` | [[Daily Task]] |
| AI Plan Generation | Splitting a goal into stations via an LLM | [[AI Plan Generation]] |
| Plan Adaptation | Adjusting the plan to actual progress | [[Plan Adaptation]] |
| Streak | Consecutive days with activity | [[Streak]] |
| Coins | In-app currency, `User.money` | [[Coins]] |
| XP | Experience points | [[Experience Points]] |
| Level | Derived from XP, 250 XP per level | [[Level]] |
| Achievement | Badge for a statistics threshold | [[Achievement]] |
| Roadmap | Visualization of a goal's stations | [[Roadmap]] |
| Progress Analytics | Stats per day / week / month | [[Progress Analytics]] |

## Technical terms
| Term | Definition | See also |
|---|---|---|
| JWT | JSON Web Token — signed token carrying user data | [[ADR-002 JWT Access and Refresh Tokens]] |
| Access token | Short-lived JWT for API requests | [[Auth Middleware]] |
| Refresh token | Long-lived token used to obtain a new access token | [[Auth Module]] |
| ORM | Object-Relational Mapping; Prisma in this project | [[Prisma Data Layer]] |
| Migration | Versioned DB schema change | [[Prisma Data Layer]] |
| Gemini | Google LLM that generates plans | [[ADR-001 Google Gemini as AI Provider]] |
| Prompt | Text instruction for an LLM | [[AI Module]] |
| Middleware | Express function between request and controller | [[Auth Middleware]] |
| Harness | Environment, tools and rules for the AI agent working on the project | [[ADR-004 Separate Knowledge Base Repository]] |
| Vault | Obsidian directory of Markdown notes | [[MOC Goals Achiever]] |
| MOC | Map of Content — hub note of links | [[MOC Goals Achiever]] |
| ADR | Architecture Decision Record | [[ADR-001 Google Gemini as AI Provider]] |

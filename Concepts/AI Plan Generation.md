---
type: concept
created: 2026-10-20
tags: [concept, ai]
related: [Goal, Station, Daily Task, Plan Adaptation, Coins]
---
# AI Plan Generation

## Definition
Automatic breakdown of a [[Goal]] into [[Station|stations]] with recommended due dates using an external LLM (Google Gemini, see [[ADR-001 Google Gemini as AI Provider]]).

## Flow
1. The user enters the goal title, deadline and context.
2. The backend builds a prompt ("You are a JSON generator…") requesting JSON `{ tasks: [{ title, description, dueDate }] }`.
3. The response is stripped of the ```json wrapper and parsed.
4. Balance is checked: plan generation costs 10 [[Coins]].
5. Tasks are saved to the DB and the balance is decremented.

## Invariants / risks
- AI API unavailability must not corrupt already saved data (non-functional requirement "Reliability").
- The LLM may return invalid JSON → parse errors must be handled.
- Fallback — manual plan creation (`ManualGenarationForm`).

## Implemented in
[[AI Module]].

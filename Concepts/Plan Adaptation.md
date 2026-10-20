---
type: concept
created: 2026-10-20
tags: [concept, ai]
related: [AI Plan Generation, Daily Task, Station]
---
# Plan Adaptation

## Definition
Adjusting the future plan according to the user's actual progress (functional requirement #8).

## Current implementation
Adaptation happens at the [[Daily Task]] level: when generating, the AI receives the current [[Station]] title and the list of already completed daily tasks, so the next tasks build on the real state rather than the initial plan.

## Planned
Regenerating the remaining stations when the user systematically misses `dueDate`.

## Implemented in
[[AI Module]] (`getProgressInfo`, `generateDailyTasks`).

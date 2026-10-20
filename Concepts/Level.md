---
type: concept
created: 2026-10-20
tags: [concept, gamification]
related: [Experience Points]
---
# Level

## Definition
User level, filled by [[Experience Points|XP]].

## Formula
- 250 XP per level;
- `level = floor(xp / 250) + 1`;
- `progressPercent = (xp % 250) / 250 × 100`.

## Implemented in
`frontend/src/pages/ProfilePage/ProfilePage.tsx`.

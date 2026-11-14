---
type: decision
created: 2026-10-20
status: accepted
tags: [decision, adr, ai]
related: [AI Module, AI Plan Generation]
sources: ["practical work 5: record-adr duplicate check, grep of backend/src (branch feature/pw5-skills)"]
---
# ADR-001 Google Gemini as AI Provider

## Context
An external LLM is needed for [[AI Plan Generation]]. Non-functional requirement "Cost" — prefer free services. Training our own model is out of scope.

## Decision
Google Gemini API (`gemini-2.5-flash`) via the `@google/genai` SDK, free tier.

## Alternatives considered
- OpenAI API — no permanent free tier;
- Anthropic Claude API — paid;
- local model (Ollama) — hard to deploy on free hosting.

## Consequences
- Free-tier limits → AI requests "cost" [[Coins]] to limit frequency.
- The response is JSON as text, so parse errors must be handled robustly.

- Checked 2026-11-14 (practical work #5): `backend/src/modules/ai/ai.service.ts` is the only LLM caller and uses `GoogleGenAI` from `@google/genai` with `gemini-2.5-flash`. `backend/package.json` also lists `@google/generative-ai`, `@mistralai/mistralai`, `genai` and `@xenova/transformers`, but nothing in `src/`, `analytics/` or `prisma/` imports them. They are leftovers, **not** additional providers. Removing them is a dependency change (guardrail W3) and needs human approval.

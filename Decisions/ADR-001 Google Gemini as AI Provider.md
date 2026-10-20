---
type: decision
created: 2026-10-20
status: accepted
tags: [decision, adr, ai]
related: [AI Module, AI Plan Generation]
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

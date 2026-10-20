---
type: decision
created: 2026-10-20
status: accepted
tags: [decision, adr, harness]
related: [MOC Goals Achiever]
---
# ADR-004 Separate Knowledge Base Repository

## Context
The agent needs a knowledge base about the app (the knowledge layer of the harness). Neo4j / Chroma require a server.

## Decision
An Obsidian vault in a **separate** git repository `goals_achiever-vault`, physically outside the app repository.

## Alternatives considered
- `docs/` folder in the app repository — mixes knowledge history with code history;
- Neo4j / Chroma — server infrastructure and costs.

## Consequences
- Independent change history for knowledge; the vault can be plugged into several tools.
- Links to code are plain-text paths, not wiki links (see README, convention #7).
- Basis for the connectors in practical work #3.

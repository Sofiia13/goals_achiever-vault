---
type: decision
created: 2026-11-14
status: accepted
tags: [decision, adr, repository, security]
related: [ADR-004 Separate Knowledge Base Repository]
sources: ["PR #1 (initial commit, merged 2025-11-15)"]
---
# ADR-008 Repository Ignore Rules

## Context
PR #1 "initial commit" (`dev` → `main`, merged 2025-11-15, commit `21085b9`) added the whole project. In the same PR the root `.gitignore` was cut from the 24-line Vite default (logs, `node_modules`, `dist`, `dist-ssr`, `*.local`, `.vscode/*`, `.idea`, `.DS_Store`, …) down to one line: `.env`. As a result, `backend/node_modules/**` was committed to the repository.

## Decision
The root `.gitignore` is the only ignore file. The minimum rule is that secrets (`.env`) must never be committed.

## Alternatives considered
- Keep the Vite default `.gitignore`: it would have covered the frontend build output and the editor/OS files.

## Consequences
- Dependencies were committed (`backend/node_modules`), which made the repository bigger and the diffs noisy.
- OS and editor files (`.DS_Store`) and build output (`dist`) are not ignored.

## Related
- [[ADR-004 Separate Knowledge Base Repository]]

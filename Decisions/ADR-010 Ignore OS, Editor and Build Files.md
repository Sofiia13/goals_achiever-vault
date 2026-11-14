---
type: decision
created: 2026-11-14
status: accepted
tags: [decision, adr, repository, security]
related: [ADR-004 Separate Knowledge Base Repository]
supersedes: [ADR-008 Repository Ignore Rules]
sources: [commit edbbc7d; practical work 4]
---
# ADR-010 Ignore OS, Editor and Build Files

## Context
[[ADR-008 Repository Ignore Rules]] recorded that the root `.gitignore` covered only `.env` and `node_modules/`. It left an open problem: `.DS_Store`, `dist/` and logs were not ignored, so OS files kept appearing in `git status` and in commits.

## Decision
The root `.gitignore` ignores four groups of files:
- secrets: `.env`;
- dependencies: `node_modules/`;
- build output and logs: `dist/`, `*.log`;
- OS and editor files: `.DS_Store`, `.vscode/*` (except `.vscode/extensions.json`), `.idea`;
- local harness logs: `.claude/logs/`.

Files that were already tracked are removed from the index with `git rm --cached`. Secrets are also guarded at runtime: the agent hook blocks reading and printing `.env` (guardrail B1), and the git pre-commit hook rejects a staged `.env`.

## Alternatives considered
- Keep ADR-008 and append to it: rejected, because the decision itself changed (from "only `.env`" to a full ignore policy). An ADR records one decision, so a new ADR supersedes the old one.
- A global `~/.gitignore` for `.DS_Store`: rejected, because it works only on one machine and is not versioned with the project.

## Consequences
- Commit `edbbc7d` (2026-11-14) extended `.gitignore`, but its message says ".DS_Store untracked" while the root `.DS_Store` stayed in the index. It is untracked on branch `feature/pw4-ontology-guardrails` (practical work #4).
- ADR-008 has status `superseded`. It is kept as history and is never deleted (guardrail B3).

## Relations
- supersedes → [[ADR-008 Repository Ignore Rules]]

## Related
- [[ADR-004 Separate Knowledge Base Repository]]

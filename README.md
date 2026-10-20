---
type: moc
created: 2026-10-20
tags: [moc, conventions]
---
# Goals Achiever — Knowledge Base

Obsidian vault with technical knowledge about the [Goals Achiever](https://github.com/Sofiia13/goals_achiever) app. It is the knowledge layer of the AI agent harness (Claude Code). The vault lives in its own repository, separate from the app repository — see [[ADR-004 Separate Knowledge Base Repository]].

**Entry point:** [[MOC Goals Achiever]].

## Structure

| Folder | Contents | `type` in frontmatter |
|---|---|---|
| `Concepts/` | domain concepts | `concept` |
| `Components/` | modules and components of the codebase | `component` |
| `Decisions/` | architecture decisions (ADR) | `decision` |
| `Glossary/` | project glossary | `glossary` |
| `Templates/` | note templates (not knowledge) | — |

## Conventions

1. **File names** — Title Case, full words, no abbreviations (`Daily Task.md`, not `dtask.md`).
2. **ADRs** are named `ADR-NNN Short Title.md` with sequential numbering.
3. **Frontmatter is mandatory** in every note; `type` is one of `concept | component | decision | glossary | moc`.
4. **Relations are expressed only via `[[wiki links]]`**, never as plain-text mentions. Related notes are also listed in the `related` field.
5. Every note must be reachable from [[MOC Goals Achiever]]. New note → add a link to the MOC.
6. Component `status`: `implemented | partial | planned`; decision `status`: `proposed | accepted | superseded`.
7. Code paths are relative to the app repository root (`backend/src/...`).

### Frontmatter templates
Stored in `Templates/` (Obsidian → Settings → Templates → Template folder location = `Templates`).
- [[Concept Template]] — `type, created, aliases, tags, related`
- [[Component Template]] — `type, created, layer, status, path, tags, related`
- [[Decision Template]] — `type, created, status, tags, related`
- [[Glossary Template]] — `type, created, tags`

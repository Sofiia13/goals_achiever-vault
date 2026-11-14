---
type: decision
created: 2026-11-14
status: accepted
tags: [decision, adr, harness, mcp]
related: [ADR-004 Separate Knowledge Base Repository, MOC Goals Achiever]
sources: ["commit cc454eb (feat(harness): add vault MCP connector and GitHub MCP config)"]
---
# ADR-007 MCP Connectors for Knowledge Base Access

## Context
The vault lives in a separate repository outside the IDE workspace ([[ADR-004 Separate Knowledge Base Repository]]). The agent needs a controlled way to read and update it, and needs commit / PR history of the app as a data source.

## Decision
- An **own MCP server** `harness/vault-mcp` (Node.js, `@modelcontextprotocol/sdk`, stdio), registered in `.mcp.json` of the app repo. Tools: `ingest_note` (create/update → commit → push, idempotent), `get_note`, `search_notes`, `vault_status`.
- The **official GitHub MCP server** (remote, `api.githubcopilot.com/mcp/`) with `X-MCP-Toolsets: repos,pull_requests` and `X-MCP-Readonly: true`. A fine-grained PAT is used: one repository, read-only, taken from the env variable `GITHUB_PAT`.
- `.claude/settings.json` lets read tools run without a prompt, makes `ingest_note` ask for confirmation, and denies direct `Read`/`Edit`/`git -C` on the vault clone.

## Alternatives considered
- Bash scripts called by the agent: they have no typed contract, and the agent can bypass them.
- A vault folder inside the app repo: this breaks [[ADR-004 Separate Knowledge Base Repository]].
- Own GitHub integration via `gh`/REST: duplicates a maintained server.

## Consequences
- Every vault change is a commit with a `Source:` line, so it can be traced.
- Repeated ingestion does not create duplicates (content comparison; ADRs are matched without their number).
- The token gives read access to one repository only.

## Related
- [[MOC Goals Achiever]]

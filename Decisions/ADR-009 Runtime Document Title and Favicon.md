---
type: decision
created: 2026-11-14
status: accepted
tags: [decision, adr, frontend, deploy]
related: [Auth Context]
sources: ["commits 71fc7b9, 61f9cfc (2026-03-30)"]
---
# ADR-009 Runtime Document Title and Favicon

## Context
On 2026-03-30 there were seven commits in a row about the favicon and page title on Vercel (`ff6c2bd` add favicon → `c268fc0`, `6d44527`, `5402059` trigger vercel redeploy, `7030b18`, `e48528f`, `71fc7b9`, `61f9cfc`). After redeploys the static `<link rel="icon">` and `<title>` in `index.html` were not picked up, most likely because of caching.

## Decision
`frontend/src/main.tsx` sets the branding at runtime, before React renders (`applyDocumentBranding()`):
- `document.title = "Goals Achiever"`;
- it finds `link[rel='icon']` or creates it, then sets `href` to `/icons/favicon.svg?v=2`.
`71fc7b9` first used an inline `data:image/svg+xml` icon. `61f9cfc` replaced it with a file in `frontend/public/icons/` and a cache-busting query `?v=2`.

## Alternatives considered
- Only static tags in `index.html`: these were cached, which was the original problem.
- An inline data-URI SVG: it worked but kept the icon inside the code (replaced in `61f9cfc`).

## Consequences
- To change the icon, update the file and raise `?v=N`.
- The title and icon are set by JS. Before the bundle loads (and for crawlers without JS) the values from `index.html` are used, so keep them in sync.

## Related
- [[Auth Context]]

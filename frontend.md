# Frontend Appendix

Append these rules to `AGENTS.md` for **frontend-only / SSG / SPA** projects (no server-side business logic, no database). Examples: Vite SPA, Next.js SSG, VitePress docs site, client-side chart tool.

## Build & Rendering

- If SSG (e.g. Next.js App Router SSG, VitePress): every page must build statically. Missing frontmatter or missing assets should degrade gracefully (warn + skip), never break the build.
- Build commands run at the **repo root** only. `cd` into a subdir and relative paths lose their anchors; `docs:build` / `git` will misreport.
- Dev server runs at a fixed port (e.g. `localhost:3000` or `localhost:5173`); don't change the port or spawn random services.

## Content / Knowledge Base (if applicable)

- Content docs require frontmatter (`title`, `description`); missing fields degrade to filename or first H1.
- Anchor links must scroll the page to the real target heading, not just update the URL bar.
- Images/SVG referenced in docs must be committed to the repo before being referenced; a missing asset breaks the docs build.
- If content lives in a git submodule, never edit it in-place from the host repo; changes go to the submodule's own repo.

## i18n

- Primary README is English; translations live in sibling files (e.g. `README.zh-CN.md`) with a top language-switch link.
- UI strings use the project's dictionary/i18n system; no hardcoded user-facing strings in components when a dictionary exists.

## Responsive & Mobile

- Mobile-first. No horizontal scrollbars at 320px width — wrap rows, collapse low-frequency controls into "more".
- UI changes must state how they were verified on both desktop and mobile.

## Assets & Proxy

- Client requests use fixed path prefixes (e.g. `/api`, `/ws`) so production proxy swaps need zero code change.
- Assets committed under `public/` (or per-chapter `_assets/` for docs); build copies them to the served location.

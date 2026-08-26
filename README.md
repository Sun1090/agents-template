# agents-template

A reusable `AGENTS.md` template for AI-agent-friendly repositories. Copy it into a new project, fill in the `<TODO>` placeholders, and you get a consistent agent entry point in minutes.

## What's inside

| File | Purpose |
|---|---|
| [`AGENTS.md`](AGENTS.md) | The main template — copy this into your repo root and fill in placeholders. |
| [`frontend.md`](frontend.md) | Appendix for frontend-only / SSG / SPA projects. |
| [`backend.md`](backend.md) | Appendix for backend / API service projects. |
| [`fullstack.md`](fullstack.md) | Appendix for fullstack projects (frontend + backend in one app). |

## How to use

1. **Copy `AGENTS.md`** into your new repo's root.
2. **Pick one appendix** based on project type and either append its rules into `AGENTS.md` or keep it as a linked file in your repo.
3. **Fill in every `<TODO>` / `<!-- ... -->` placeholder** — project description, repo layout, commands, deployment, database.
4. **Delete what doesn't apply.** No database? Remove the `## Database` section. No i18n? drop that rule.
5. **Keep auto-generated blocks.** If the project uses Next.js, `next dev` re-adds a `<!-- BEGIN:nextjs-agent-rules -->` block at the bottom — leave it; committing it keeps the tree clean.

## Choosing an appendix

| Project type | Appendix | Example stacks |
|---|---|---|
| Frontend-only / SSG / docs site | `frontend.md` | Next.js SSG, Vite SPA, VitePress |
| Backend / API service | `backend.md` | Express, Hono, Fastify, Nitro API |
| Fullstack (one app, FE+BE) | `fullstack.md` | Next.js App Router + RSC, Nuxt + Nitro, SaaS template |

If the project has both a client app and a separate API service, use `frontend.md` for the client repo and `backend.md` for the API repo.

## Conventions baked in (override if your project differs)

- **Commit:** Conventional Commits, no `Co-Authored-By` / AI sign-off, one logical topic per commit.
- **Pre-push gate:** lint + typecheck + test + **build** (build is mandatory for fullstack/i18n projects).
- **Working-tree hygiene:** stage only files for the current task; never sweep in unrelated uncommitted changes.

## Reference: real projects this was distilled from

| Project | Type | Appendix used |
|---|---|---|
| trade-buty | Frontend SSG + content submodule | `frontend.md` (+light backend notes) |
| kline-buty | Pure frontend + VitePress docs | `frontend.md` |
| labor-dispatch-admin | Fullstack Nuxt admin | `fullstack.md` |
| IndieStack | Fullstack SaaS (Next.js + Supabase) | `fullstack.md` |

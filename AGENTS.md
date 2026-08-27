# AGENTS.md

This file is the entry point for AI agents working in this repository. It routes to concrete rules; do not pile every detail here. Keep it scannable, delegate specifics to linked docs.

## Project

<!-- One sentence: what this project is and who it serves. -->
<!-- Example: <Project Name> is a <type> application for <audience>. -->

_TODO: fill in one-sentence project description._

## Required Reading

Read in order before making changes:

1. [`README.md`](README.md) — product capabilities, tech stack, quick start.
2. <!-- Link to architecture/plan doc if exists, e.g. `docs/plan.md`. -->
3. Before writing code: read this file end to end; framework-specific notes may appear in an auto-generated block at the bottom.

## Repository Layout

<!-- Describe top-level dirs. Example:
- App code: `src/app/`, `src/lib/`
- Database: `<db path>`
- Scripts: `scripts/`
- Docs: `docs/`
-->

_TODO: fill in repository layout._

## Commands

<!-- Replace with actual package manager + script names. -->

```bash
<pm> install          # install dependencies
<pm> run dev          # dev server
<pm> run build        # production build
<pm> run lint         # lint
<pm> run typecheck    # type check (or type-check)
<pm> run test         # tests
```

## Reuse First

Prefer what's already installed over hand-rolled code: check `package.json` for a dependency that covers the need before writing your own, and grep the repo for an existing util/helper/component before creating a new one. Prefer built-in APIs (native `fetch`, framework server actions, middleware) over adding a dependency for the same job. Add a new dependency only when nothing fits, and state why in the PR.

## Code Style

- Use the project's pinned runtime and package manager (e.g. Node 22 + pnpm 10, or Node 22 + npm).
- Follow the ESLint/Prettier config; run lint before requesting review.
- Prefer explicit types over `any`.
- Keep functions and handlers small; extract reusable logic into `utils/` or `services/`.
- Name files in English, no numeric prefixes (unless this repo states otherwise).
- No hardcoded secrets or insecure fallbacks.
- No unused imports or debug logging left behind.
- Do not log credentials, password hashes, cookies, tokens, or full database rows.

## Testing & Quality Gates

- Add or update tests for permission behavior, security-sensitive logic, and reusable utilities.
- Run lint + typecheck + test + build before review and before every push.
- CI runs the same checks; a red gate blocks merge until fixed or explicitly time-boxed by the maintainer.
- If the project has i18n: run the locale key-symmetry check before push (missing keys often surface only at build time).

## Commit Convention

- Conventional Commits: `<type>(<scope>): <subject>`.
  - Types: `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `build`, `ci`, `chore`, `revert`.
  - Subject: concise, no trailing period, ≤ 72 chars.
- **No `Co-Authored-By` or any AI sign-off.** Author is the human maintainer only.
- One commit = one logical topic. Don't mix unrelated changes.

## Git & Review

- Keep changes focused and incremental.
- Stage only files related to the current task; never sweep in unrelated uncommitted work from the working tree.
- Do not commit generated build output, local environment files, or another contributor's uncommitted work without confirmation.
- Single-maintainer workflow (if applicable): commit directly to `main`; all local quality gates MUST pass before every push.

## Deployment

<!-- Example: default target is a long-running Node server; apply migrations only from a trusted operator environment. -->

_TODO: fill in deployment target and commands._

## Database

<!-- If applicable. Example:
- Treat schema file + committed migrations as source of truth.
- Use migrations for schema changes; no schema push against shared/prod databases.
- Keep seed scripts idempotent and transactional.
-->

_TODO: fill in database conventions, or remove this section if no backend._

## Appendix (by project type)

Pick **one** of the following and append its rules to this file (or keep it linked):

- **Frontend-only / SSG** → [`frontend.md`](frontend.md)
- **Backend / API service** → [`backend.md`](backend.md)
- **Fullstack (frontend + backend in one app)** → [`fullstack.md`](fullstack.md)

<!-- If this project uses Next.js, an auto-generated rules block may be appended below by `next dev`. Keep it. -->

# AGENTS.md

This file is the entry point for AI agents working in this repository. It routes to concrete rules; do not pile every detail here. Keep it scannable, delegate specifics to linked docs.

## Autonomous Execution and Branch Lifecycle

- Work continuously from repository evidence: inspect → choose the highest-priority executable task → implement → test → fix → verify → commit → update progress → inspect again. Do not stop merely because one task, commit, PR, release, or milestone is complete.
- Before coding, inspect the roadmap/milestones, TODO/FIXME markers, CI/build/test status, and `docs/progress.md`; create `docs/progress.md` when the repository uses no equivalent progress log.
- Prioritize blockers, failing quality/security gates, core bugs, milestone critical paths, tests/migrations, performance/CI, dependencies/security, then documentation. Fix discovered issues when feasible instead of only recording them.
- Stop only when all executable work is complete, a product decision or credential/external permission is required, an upstream dependency blocks every remaining task, or a hard tool/context limit prevents further progress.
- Use a focused topic branch and atomic Conventional/Angular commits unless this repository explicitly requires direct-to-main development. Rebase with `git fetch origin && git rebase origin/<base>`; never create merge commits, force-push, rewrite shared history, or change repository protection rules.
- **Remote topic branches are temporary PR transport, not persistent storage.** Do not push `codex/*`, `feat/*`, or any other topic branch merely for backup/checkpoints. Push one only when opening or updating its PR. After a PR is merged or closed, delete its remote branch immediately and prune stale tracking refs. Before starting another branch, audit open PRs and remote branches; finish/merge viable work and remove branches already merged.
- Never push directly to `main`/`master` when the repository uses protected-branch PR review. Where direct-to-main is explicitly documented, that repository-specific rule takes precedence.
- Keep `docs/progress.md` (or the repository equivalent) current with milestone/version, status, branch/commit, completed work, changed files, verification, blockers, risks/rollback, next task, and update date.

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
- Use a short-lived topic branch and pull request; never push directly to `main`/`master`. Delete the remote topic branch immediately after merge or closure.

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

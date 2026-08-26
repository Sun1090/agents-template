# Fullstack Appendix

Append these rules to `AGENTS.md` for **fullstack** projects — one app with both frontend and backend (e.g. Next.js App Router with RSC + Server Actions, Nuxt with Nitro, SaaS templates with Supabase). Inherits concerns from both [`frontend.md`](frontend.md) and [`backend.md`](backend.md); this file adds the intersection rules.

## Rendering Model

- Default to Server Components / server-rendered pages. Add `"use client"` (or client directive) only when interactivity is needed (useState, useEffect, event handlers).
- Write operations (create/update/delete) go through Server Actions (or the framework equivalent). API routes stay for external callbacks only — don't duplicate the same business logic as both an Action and an API route.

## Data Access Layer

- Table queries flow through a repository layer (`lib/repositories/<table>.ts` or `server/services/`). New queries go into the repository; no direct `.from()` in components or actions.
- Server components use the server client; client components use a hook (e.g. `useUser()`); admin operations use a service-role client. Don't mix them up.

## Auth & RLS

- If the DB supports Row Level Security (Supabase/PostgreSQL): keep RLS enabled on all tables; client queries are scoped by RLS, admin queries bypass it via the service-role client only in trusted server contexts.
- Route guards: `requireAuth()` → redirect when unauthenticated; `requireRole(minRole)` / `requirePermission(perm)` for finer control. Client gates (`PermissionGate`) are UX only.

## Validation

- Forms and API input validated with Zod (or equivalent). Shared schemas in `lib/validations/` (or `shared/validations/`).
- Server Actions return a unified result shape (e.g. `ActionResult`) so the client can render success/error uniformly.

## i18n

- Server: translation function from the i18n runtime (e.g. `next-intl/server`). Client: `useTranslations()`. Translation files in `messages/` (JSON); keep `zh-CN` and `en` key-symmetric — missing keys surface only at `build`, so **`build` is a mandatory pre-push gate**.

## Pre-push Gate (fullstack-specific)

Every `git push` must pass in order:

```bash
<pm> lint
<pm> type-check     # or typecheck
<pm> test
<pm> build          # ← critical: i18n missing keys / SSG errors only surface here
```

Skipping `build` before push is treated as an incident.

# Backend Appendix

Append these rules to `AGENTS.md` for **backend / API service** projects. Examples: Nuxt/Nitro server, Express, Hono, Fastify.

## Architecture

- Keep server handlers small; extract reusable logic into `server/utils/` or `server/services/`.
- API routes are for external-service callbacks (webhooks, OAuth), health checks, and cases that genuinely need an HTTP endpoint. Don't maintain a Server Action and an API route for the same business logic.

## Authentication & Authorization

- Authn and authz are enforced **server-side**. Client-side checks are UX only.
- Protected handlers require an authenticated user and the least-privilege permission for the operation.
- Use centralized permission helpers; no scattered string comparisons for roles.
- Secrets (`DATABASE_URL`, `JWT_SECRET`, service-role keys) come from the deployment environment; never commit real credentials or `.env` files.

## Database

- Treat the schema file + committed migrations as the source of truth.
- Use migrations for schema changes; no `schema push` against shared or production databases.
- Apply migrations only from a trusted operator environment.
- Keep seed scripts idempotent and transactional where possible.

## Logging & Security

- Never log credentials, password hashes, cookies, tokens, or full database rows.
- Validate input at the boundary (Zod / class-validator / etc.).
- Return correct HTTP status codes; wrap handlers in try/catch.
- Rate-limit auth-sensitive endpoints; webhook routes rely on signature verification (not in-memory rate limits).

## Deployment

- Default target is a long-running Node server (e.g. Nitro `node-server` preset). Start with `node .output/server/index.mjs` or equivalent.
- Serverless targets need an explicit preset and a persistent storage strategy for uploads/backups.

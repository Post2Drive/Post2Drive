# Post2Drive repository and Railway staging status

**As of 17 October 2026**

## Repository roles

- [Post2Drive/post2drive-app](https://github.com/Post2Drive/post2drive-app) — canonical app source. The complete prepared source bundle has been imported into `main`; Next.js pages and API routes are under the correct `app/` directory.
- [Post2Drive/Post2Drive](https://github.com/Post2Drive/Post2Drive) — project overview and release notes. Keep app code in the canonical application repository, not duplicated here.

## Verified source and CI

- Source archive SHA-256: `19c34528045b717ef5f6e7546f028a884ece41414073ac13c22b51d6b88a91fc`
- Latest source commit deployed to staging: `ddad7102ef105732f9ae0ac0ea7cae5ca37ccdae` — `fix: filter non-null market research with Prisma DbNull`
- GitHub Validate: [passed](https://github.com/Post2Drive/post2drive-app/actions/runs/38950482164)

The successful validation run completed dependency installation, targeted reliability/health/lifecycle/market/timezone contract checks, Prisma schema validation and client generation, clean-database migrations, isolated `staging`-schema migration checks, read-only QA cleanup inventory validation, TypeScript type-checking, and the Next.js production build.

Two Prisma JSON-null type errors were corrected using `Prisma.DbNull` for the nullable market-research field. The latest commit above includes both fixes and is the source deployed below.

## Railway staging inventory

Private project: **Post2Drive Staging**  
Project ID: `074d55f7-6a58-4c46-86aa-a2c7b0079859`  
Environment: **staging only**  
Environment ID: `293eb264-dd1d-4eef-87ca-016943459edf`

| Service | Service ID | Current verified state |
|---|---|---|
| Postgres | `4fb4f66a-9869-4976-bc29-217efe0104f4` | Online; deployment succeeded; persistent volume |
| Redis | `47efbd4e-f432-4fa1-91eb-a809c26d9f80` | Online; deployment succeeded; persistent volume; not used by app code yet |
| Post2Drive Web | `561c5355-867e-49fc-84bf-e519e1ac8ef0` | **Online; deployment succeeded**; source is `Post2Drive/post2drive-app` `main` |
| Post2Drive Infra Smoke Test | `04107a5c-3b23-4d89-8864-af75355530a3` | Function deployment succeeded; separate infrastructure-only check |

### Staging URLs

Marketplace: https://post2drive-web-staging.up.railway.app  
Marketplace health: https://post2drive-web-staging.up.railway.app/api/health

Infrastructure smoke test: https://post2drive-infra-smoke-test-staging.up.railway.app  
Infrastructure health: https://post2drive-infra-smoke-test-staging.up.railway.app/api/health

The web deployment ID is `a19e8fd0-fb4a-4154-9534-81d2887cf83b`. Railway reports deployment status `SUCCESS`, service state `Online`, no active issues, and no pending deployment work. The container started Next.js 15.5.27 successfully. Railway's configured GET `/api/health` deployment check succeeded.

The pre-deploy command `npx prisma migrate deploy` ran and reported: **All migrations have been successfully applied.** The production build completed successfully before image push and deployment.

The separate smoke-test page is **not the marketplace**. Its POST health probe previously returned HTTP 200 only when PostgreSQL `SELECT 1` and Redis `PING` both succeeded. Redis remains provisioned but not yet integrated into application code.

## App configuration and health

The web service is configured for `npm run build`, `npx prisma migrate deploy`, `npm run start`, and the `/api/health` health check on port 3000. It references PostgreSQL and Redis through Railway variable references. A staging-only NextAuth secret is configured. Email verification is disabled in staging because no sender/provider key is configured; this is for isolated tests only and is not a production recommendation.

## Remaining release gates

The source is built and deployed to **staging**, but Post2Drive is still **not production-ready**. Before wider tester access:

1. Run browser-based signup/login checks and verify UK/GBP versus India/INR separation with synthetic data.
2. Exercise job posting, bidding, accept/cancel transitions, delivery status, notification flows, incidents and evidence handling.
3. Test account deletion and verify access is disabled and personal account details are anonymised as expected.
4. Configure and verify a real email sender before enabling email verification.
5. Keep real payments disabled until a provider adapter, signature verification, idempotency, failure/replay/refund handling and reconciliation are tested.
6. Add/verify backups, alerting, operational monitoring, incident response and production data isolation before promotion.

Do not use production customer data or credentials in staging. Do not force-push, connect to the retired production database, or promote the staging deployment to production before the release gates pass.

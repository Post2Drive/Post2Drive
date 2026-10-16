# Post2Drive repository and Railway staging status

**As of 16 October 2026**

## Repository roles

- [Post2Drive/post2drive-app](https://github.com/Post2Drive/post2drive-app) — canonical app source. It currently contains bootstrap documentation only; the full application source must still be pushed from the prepared source ZIP.
- [Post2Drive/Post2Drive](https://github.com/Post2Drive/Post2Drive) — project overview and release notes. Keep app code in the canonical application repository, not duplicated here.

## Railway staging inventory

Private project: **Post2Drive Staging**  
Project ID: 074d55f7-6a58-4c46-86aa-a2c7b0079859  
Environment: staging  
Environment ID: 293eb264-dd1d-4eef-87ca-016943459edf

| Service | Service ID | Current state |
|---|---|---|
| Postgres | 4fb4f66a-9869-4976-bc29-217efe0104f4 | Online; deployment succeeded; persistent volume |
| Redis | 47efbd4e-f432-4fa1-91eb-a809c26d9f80 | Online; deployment succeeded; persistent volume; not used by app code yet |
| Post2Drive Web | 561c5355-867e-49fc-84bf-e519e1ac8ef0 | Configured; no source or app deployment |
| Post2Drive Infra Smoke Test | 04107a5c-3b23-4d89-8864-af75355530a3 | Function deployment succeeded; domain assigned |

Infrastructure smoke-test URL: https://post2drive-infra-smoke-test-staging.up.railway.app  
Health JSON: https://post2drive-infra-smoke-test-staging.up.railway.app/api/health

The temporary page is explicitly labeled as an infrastructure check, not the marketplace. It checks PostgreSQL SELECT 1 and Redis PING without exposing secrets or raw connection errors. Railway reports a successful deployment/domain assignment, but independent external HTTP reachability has not yet been confirmed from available fetch tools.

Reserved marketplace URL: https://post2drive-web-staging.up.railway.app

The web URL is assigned to the existing web service on port 3000, but that service has no application source/deployment. It will serve the product only after the source is imported, CI passes, and the existing service is connected to the app repository in the staging environment.

## App configuration and health

The web service is configured for npm run build, npx prisma migrate deploy, npm run start, and /api/health. It references PostgreSQL and Redis through Railway private variable references. A staging-only NextAuth secret is set. Email verification is disabled in staging because no sender/provider key is configured; this is only for isolated tests and is not a production recommendation.

The prepared source bundle includes a non-sensitive database-aware GET /api/health endpoint and CI contract check. It should return HTTP 200 only when PostgreSQL can be reached.

## Verification status

Targeted checks pass for market/currency isolation, UK/India timezone and DST edges, lifecycle/market guards, reliability-budget calculations, health endpoint contract, and ZIP integrity/exclusions. Full dependency installation, Prisma validation/migrations, TypeScript and Next.js production build remain unverified. The app source is not yet in GitHub, so the application Validate workflow has not run.

## Next release gates

1. Copy the full prepared ZIP into a clone of post2drive-app; inspect staged files, then push without force.
2. Confirm GitHub Actions passes dependency installation, migrations, type-checking and production build.
3. Connect the existing Post2Drive Web service to the app repository's main branch in the staging environment only.
4. Confirm migration, build, app healthcheck and browser requests succeed. Use synthetic accounts/data only.
5. Complete browser/mobile, account-deletion, cross-market authorization, incident evidence, and notification tests before wider tester access.
6. Configure email credentials only after a verified sender is available. Keep live payments disabled until a real provider adapter with signature verification, idempotency, failure/replay/refund handling and reconciliation is tested.

Do not use production customer data or credentials in staging. Do not force-push, connect to the retired production database, or promote the app before its release gates pass.

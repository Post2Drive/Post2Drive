# Post2Drive repository and Railway staging status

**As of 16 October 2026**

## Repository roles

- [Post2Drive/post2drive-app](https://github.com/Post2Drive/post2drive-app) — canonical app source. It currently contains bootstrap documentation only; the complete application source must still be pushed from the prepared source ZIP.
- [Post2Drive/Post2Drive](https://github.com/Post2Drive/Post2Drive) — project overview and release notes. Keep app code in the canonical application repository, not duplicated here.

## Railway staging inventory

Private project: **Post2Drive Staging**  
Project ID: 074d55f7-6a58-4c46-86aa-a2c7b0079859  
Environment: staging  
Environment ID: 293eb264-dd1d-4eef-87ca-016943459edf

| Service | Railway service ID | Status |
|---|---|---|
| Postgres | 4fb4f66a-9869-4976-bc29-217efe0104f4 | Deployment succeeded; persistent volume attached |
| Redis | 47efbd4e-f432-4fa1-91eb-a809c26d9f80 | Deployment succeeded; persistent volume attached; not yet used by app code |
| Post2Drive Web | 561c5355-867e-49fc-84bf-e519e1ac8ef0 | Build/start/migration/healthcheck settings configured; no source or deployment |

Reserved web URL: https://post2drive-web-staging.up.railway.app

The URL is assigned to the web service on port 3000, but it is **not yet serving the application** because the service has no source or deployment. No production app or production data has been connected.

## App configuration and health

The web service references Postgres and Redis using private Railway variable references, is configured for npm run build, npx prisma migrate deploy, npm run start, and /api/health, and uses a staging-only NextAuth secret. Email verification is disabled in staging because no sender/provider key has been configured; this is for isolated tests only and is not a production recommendation.

The prepared source bundle now includes a non-sensitive database-aware GET /api/health endpoint and a CI contract check. The endpoint should return 200 only when Postgres can be reached.

## Verification status

Targeted source checks pass for market/currency isolation, UK/India timezone and DST edge cases, lifecycle/market-guard contracts, reliability-budget arithmetic, health endpoint contract, and ZIP integrity/exclusions.

The full dependency install, Prisma validation and migrations, TypeScript check, and Next.js production build remain unverified because a clean dependency install could not complete in this environment. The GitHub Actions workflow has not run: the source files are not yet in the GitHub repository.

## Next release gates

1. Copy the complete prepared source ZIP into an existing clone of post2drive-app; inspect all staged paths, then push without force.
2. Confirm GitHub Actions passes dependency installation, migrations, type-checking and production build.
3. Connect the existing Post2Drive Web service to the app repository's main branch in the staging environment only.
4. Confirm migrations, build, Railway healthcheck and browser requests succeed. Use synthetic accounts and data only.
5. Complete browser/mobile, account-deletion, cross-market authorization, incident-evidence, and notification tests before wider tester access.
6. Configure email provider credentials only after a verified sender is available. Keep live payments disabled until an actual provider adapter with signature verification, idempotency, error/replay/refund handling and reconciliation is tested.

Do not use production customer data or credentials in staging. Do not force-push, connect to the retired production database, or promote the app before its release gates pass.

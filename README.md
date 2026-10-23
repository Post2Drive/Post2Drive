> **Status audit — 23 October 2026 (GitHub verified; Railway dashboard recheck blocked).** This note supersedes older date-stamped status snapshots below where they conflict. This repository's latest `main` commit is `5c8787a4` (17 Oct). PR #2 (Founder business-validation skills) is closed without merge; PR #1 (staging-status documentation sync) is merged. The application repository is the source of truth for code. Current app-repo GitHub state: PR #43 (integration branch to main) and PR #44 (audit follow-up branch to integration) are open drafts; neither is merged. PR #12 is closed unmerged. CI on PR #44 head `21a41b45` passed Validate, Security Scan, CodeQL and Android Capacitor build on 23 Oct. These checks do not prove live staging E2E or launch readiness.
>
> **Railway limitation:** the connected Railway tools could list the project but returned a permissions error when asked to inspect the staging environment. Therefore, the live dashboard's current deployment, service health, database targets and pending changes could not be independently re-verified. Service/commit details below are the last recorded 18 Oct snapshot, not a fresh live confirmation.

# Post2Drive

**Post2Drive Logistics Network** is a UK-first freight and courier marketplace project, with UK and India markets separated at the application and data-access layers.

## Repositories

- **Application source:** [Post2Drive/post2drive-app](https://github.com/Post2Drive/post2drive-app) — canonical app source. Keep product code there.
- **Project/profile:** this repository — overview, operating posture, and release notes. Do not duplicate the app code here.

## Railway staging

The app is deployed to the private Railway project **Post2Drive Staging**, in its **staging-only** environment. This is not production approval.

- [Post2Drive marketplace — staging](https://post2drive-web-staging.up.railway.app) — the Web service is deployed from [`Post2Drive/post2drive-app`](https://github.com/Post2Drive/post2drive-app/tree/feature/country-localisation-audit), branch `feature/country-localisation-audit`, **not** `main`.
- [Marketplace health endpoint](https://post2drive-web-staging.up.railway.app/api/health) — PostgreSQL-backed health check; a successful response does not prove every workflow or the operations dashboard connection is correct.

**Verified 18 October 2026:** the latest Railway Web deployment (`07a10fe2-521d-4cff-a579-fa6b2c11fabd`) and QA-worker deployment (`2ee35307-2147-4044-a649-c714c91681a9`) both report **SUCCESS**. These deployments are on the feature branch. Its latest commit `b5b272478c7deb7d888e2e48fcedbf4d3757891a` is documentation-only; the app runtime code revision inspected was `b15e0ff754860c564db6fc26930a024d85234938`. The current candidate's CodeQL, TypeScript checks, and Railway Web/worker status checks passed. This is not a substitute for complete end-to-end or production release validation.

Railway still records earlier failed deployment attempts in its history; the newest successful deployment does not clear or erase those incidents.

### Infrastructure notes

- The Railway service still named **Post2Drive Infra Smoke Test** actually runs `npm run qa:worker`. It is a PostgreSQL-backed QA worker, has **no public domain**, and is not a public smoke-test page.
- The latest web migration logs identify `post2drive_qa` on `postgres-j8xl.railway.internal`, corresponding to service **Postgres-J8xl**, as the active staging app database.
- A separate **Postgres** service and its own persistent volume remain online. Their data ownership and consumers are unverified. Do not delete, migrate, or repoint it until its contents and all connection strings have been checked.
- The unused Redis service has been removed from active staging use because no runtime client/consumer was found. Its persistent volume is retained unattached; the volume was **not** deleted.
- The operations dashboard is intended to use a restricted `post2drive_ops_readonly` role. Its effective `OPS_DASHBOARD_DATABASE_URL` target and actual read-only permissions still need independent verification.

See [Staging and Release Status](docs/STAGING_AND_RELEASE_STATUS.md) and the [application runbook](https://github.com/Post2Drive/post2drive-app/blob/feature/country-localisation-audit/docs/RAILWAY_STAGING_SETUP.md) for service IDs, database ownership cautions, and release gates.

## Release posture

Post2Drive is in active development and is **not production-ready**. Before wider tester access or public launch, complete the browser/mobile workflow checks, verify UK/GBP and India/INR isolation, test signup/login and account deletion, confirm notifications and incident/evidence flows, establish backups and recovery, and configure operational monitoring.

Staging email verification remains disabled because a verified sender/provider is not configured. Keep real payments disabled until a provider is integrated and signature verification, idempotency, failures/replays, refunds, and settlement reconciliation are tested end to end.

## Safety principles

1. Keep staging and production credentials/data isolated.
2. Never commit `.env` files, keys, tokens, signing keys, database dumps, or personal data.
3. Use synthetic test accounts/data only on staging URLs.
4. Do not enable real payments or email verification until provider configuration and end-to-end behavior are verified.
5. Preserve strict UK/GBP and India/INR marketplace separation.
6. Do not force-push or reuse retired production infrastructure.
7. Treat staging as test-only; do not share sensitive or real customer data on it.

## Next step

Close the remaining staging verification gaps documented in [Staging and Release Status](docs/STAGING_AND_RELEASE_STATUS.md): confirm the operations-dashboard database target and read-only access, establish ownership of the separate PostgreSQL service, preserve historical failures, and complete synthetic-data browser/mobile smoke tests. Do not promote to production until launch gates are reviewed and passed.

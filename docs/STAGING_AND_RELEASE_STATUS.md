# Post2Drive repository and Railway staging status

**Status checked: 18 October 2026**

## Repository roles

- [`Post2Drive/post2drive-app`](https://github.com/Post2Drive/post2drive-app) is the canonical application source.
- This repository, [`Post2Drive/Post2Drive`](https://github.com/Post2Drive/Post2Drive), is the project overview and release-status record. Keep application code in the app repository rather than duplicating it here.
- The staging Web and QA worker services are connected to branch `feature/country-localisation-audit` in `post2drive-app`, **not** the `main` branch.
- The app branch's pull request [#12 — Audit and localise Post2Drive markets](https://github.com/Post2Drive/post2drive-app/pull/12) remains a draft. Staging success is not approval to merge that candidate to `main` or promote it to production.

## Current source and deployment evidence

- App runtime code revision last inspected: `b15e0ff754860c564db6fc26930a024d85234938`.
- The latest branch commit, `b5b272478c7deb7d888e2e48fcedbf4d3757891a`, contains documentation-only changes after that runtime revision.
- Latest Railway Web deployment: `07a10fe2-521d-4cff-a579-fa6b2c11fabd` — **SUCCESS**.
- Latest Railway QA-worker deployment: `2ee35307-2147-4044-a649-c714c91681a9` — **SUCCESS**.
- On the current branch head, the CodeQL, TypeScript, and Railway Web/worker status checks reported success. This does not equal a complete end-to-end verification or a production release approval.
- The app starts on port 3000 and the Railway Web health check uses `GET /api/health`. The health endpoint confirms PostgreSQL connectivity; it does not verify every business workflow or the separate operations-dashboard database connection.
- Railway still reports earlier failed deployment attempts in its recent history (four recent failed attempts were recorded during this review). Preserve those incidents; a successful latest deployment does not erase them.
- The environment has no staged changes or pending deployment work at the time of this check.

## Railway staging inventory

Private project: **Post2Drive Staging**  
Project ID: `074d55f7-6a58-4c46-86aa-a2c7b0079859`  
Environment: **staging only**  
Environment ID: `293eb264-dd1d-4eef-87ca-016943459edf`

| Service | Service ID | Current understanding |
|---|---|---|
| Post2Drive Web | `561c5355-867e-49fc-84bf-e519e1ac8ef0` | Online; latest deployment succeeded; source `Post2Drive/post2drive-app`, branch `feature/country-localisation-audit` |
| Post2Drive Infra Smoke Test | `04107a5c-3b23-4d89-8864-af75355530a3` | Online; actually runs `npm run qa:worker`; this is the QA worker, not a public smoke-test service |
| Postgres-J8xl | `ef2d67df-d9c9-4851-bb12-0728cf40c5da` | Online, persistent volume; observed active staging app database through Prisma deployment logs |
| Postgres | `4fb4f66a-9869-4976-bc29-217efe0104f4` | Online, separate persistent volume; contents/owner and any remaining consumers are not yet verified |

### Live staging URLs

- Marketplace: https://post2drive-web-staging.up.railway.app
- Marketplace health endpoint: https://post2drive-web-staging.up.railway.app/api/health

The service still labelled **Post2Drive Infra Smoke Test** has **no public domain** and is configured as a PostgreSQL-backed QA worker. The old `post2drive-infra-smoke-test-staging.up.railway.app` and `/api/health` smoke-test references are stale and should not be used.

### Database ownership and access — still requires verification

- The latest successful Web pre-deploy migration logs identify database `post2drive_qa` on `postgres-j8xl.railway.internal`, corresponding to **Postgres-J8xl**, as the deployed app's database. Treat it as the active staging database unless an intentional, backed-up migration is approved.
- **Postgres** is a second database service with its own volume. Its data ownership and live consumers have not been established. Do not delete, migrate, or repoint it until its schemas/data and every database connection setting—including `OPS_DASHBOARD_DATABASE_URL`—have been inspected and recorded.
- The Web pre-deploy command provisions/verifies `post2drive_ops_readonly` on the database referenced by `DATABASE_URL`, then runs `npx prisma migrate deploy`. The latest log reported no pending migrations on `post2drive_qa`.
- The operations dashboard is intended to connect using a dedicated restricted role through `OPS_DASHBOARD_DATABASE_URL`. Railway's connected configuration view redacts the effective value. Independently confirm in Railway that the variable targets the intended staging database and that its user is genuinely read-only. An HTTP 200 from the metrics route is not proof of the correct target or permissions.

### Redis and retained infrastructure

Redis was removed from the active staging services because no Redis client dependency or runtime consumer was found in the application, operations dashboard, rate limiter, or QA worker. `REDIS_URL` was blanked for Web and worker. The Redis persistent volume, `redis-volume` (`8a301634-90d4-457f-8259-f71bdfdbe5fb`), remains live but **unattached**; it was not deleted. The dashboard cache is process-local, and the QA queue is PostgreSQL-backed. Do not describe Redis as active, integrated, or responsible for current performance.

The Railway service name `Post2Drive Infra Smoke Test` is still misleading. It runs the worker command `npm run qa:worker`, uses PostgreSQL-backed queueing, and has no public domain. Rename its display name in Railway when convenient; do not recreate a public smoke-test service unless one is intentionally designed and tested.

## QA evidence and incidents

A 10,000-account staging QA attempt on 16 October failed before route-matrix execution because its synthetic signup payload omitted required `termsAccepted`, `termsVersion`, and `fleetVehicleCount` fields. The associated source fix was subsequently merged to `main` via [PR #8](https://github.com/Post2Drive/post2drive-app/pull/8) on 16 October; PR #8 is **closed and merged**, not open or in draft. Do not repeat an old QA command based only on this historical note—verify the exact source, worker revision, environment allow-list and isolated database first.

The app's launch-readiness record reports a later staging campaign with 20,000 synthetic accounts, 28,000 API-load checks, and 29,914 workflow/E2E checks. These are staging campaign counts, not a production reliability claim. The same record logged 555 raw HTTP 5xx responses in a 24-hour report; 552 were attributed to the deliberately unconfigured verification-start webhook and three remained unattributed. Recheck route-level 5xx data before clearing this gate.

The current app branch's draft localisation PR remains [#12](https://github.com/Post2Drive/post2drive-app/pull/12). Do not infer production readiness from successful deployment checks or from documentation changes.

## Remaining release gates

Post2Drive is deployed to **staging only** and is **not production-ready**. Before widening tester access or promoting a release:

1. Verify `OPS_DASHBOARD_DATABASE_URL` targets the intended staging database through the restricted `post2drive_ops_readonly` role; verify actual SELECT-only permissions.
2. Inspect the second PostgreSQL service's contents/ownership and identify every live connection consumer. Keep its volume and service intact pending that audit and a documented backup/restore decision.
3. Complete browser and mobile smoke tests using synthetic data: signup/login, country/currency isolation, posting/searching jobs, bidding/acceptance, cancellation and delivery-state transitions, notifications, incidents/evidence, and account deletion.
4. Configure a verified email sender and test delivery, token expiry/single use, resend throttling and protected actions before enabling email verification.
5. Keep real payments disabled until a provider integration is implemented and tested for signature verification, idempotency/replay, failure/cancellation/refund paths and settlement reconciliation.
6. Establish and test backups/restore, operational alerting, incident response, rollback, and database connection limits.
7. Complete legal and user-facing readiness review, including terms, privacy/data-retention notices, support contact, applicable UK GDPR handling and carrier eligibility/document requirements.
8. Verify CI and the exact source revision proposed for release. Keep production credentials/data and retired production infrastructure separate from staging.

## Safety rules

- Use synthetic accounts and data only on staging.
- Do not expose production credentials, customer records, database dumps, secrets, or tokens in code or documentation.
- Do not force-push, attach the app to a retired production database, or reuse old credentials.
- Do not delete either PostgreSQL service or the retained Redis volume until ownership, consumers, backup and retention decisions have been reviewed.
- Do not enable real payments or email verification until end-to-end provider behavior has been verified.
- Do not promote the draft feature branch to production based on a successful build or deploy alone.

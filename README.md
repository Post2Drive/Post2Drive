# Post2Drive

**Post2Drive Logistics Network** is a UK-first freight and courier marketplace project, with UK and India markets separated at the application and data-access layers.

## Repositories

- **Application source:** [Post2Drive/post2drive-app](https://github.com/Post2Drive/post2drive-app) — canonical app repository, now populated with the complete source baseline and source-import workflow.
- **Project/profile:** this repository — overview, operating posture, and release notes. Do not duplicate the application code here.

## Railway staging

The app is deployed to the private Railway project **Post2Drive Staging** in its **staging-only** environment.

- [Post2Drive marketplace — staging](https://post2drive-web-staging.up.railway.app) — deployed from `Post2Drive/post2drive-app` branch `main`.
- [Marketplace health endpoint](https://post2drive-web-staging.up.railway.app/api/health) — non-sensitive PostgreSQL-backed health status.
- [Infrastructure smoke-test page](https://post2drive-infra-smoke-test-staging.up.railway.app) — temporary status page that checks PostgreSQL and Redis connectivity.
- [Infrastructure health JSON](https://post2drive-infra-smoke-test-staging.up.railway.app/api/health) — separate infra check, not the app itself.

**Verified 17 October 2026:** Railway reports the web deployment as **SUCCESS / Online**; the pre-deploy Prisma migrations were applied; the configured `/api/health` health check succeeded; no active deployment issues or pending work were reported. The latest GitHub Validate workflow also passed dependency installation, QA contracts, Prisma schema/client generation, migrations, TypeScript checking, and the Next.js production build.

- [Successful GitHub validation run](https://github.com/Post2Drive/post2drive-app/actions/runs/38950482164)
- Latest validated source commit: `ddad7102ef105732f9ae0ac0ea7cae5ca37ccdae`

The infrastructure smoke test is **not the marketplace**; it remains a separate service. Redis is provisioned but not yet used by app code. See [Staging and Release Status](docs/STAGING_AND_RELEASE_STATUS.md) for service IDs and remaining release gates.

## Release posture

Post2Drive is in active development and is **not production-ready**. Passing build and migration checks do not replace end-to-end product verification.

Remaining release gates include real email delivery and verification, payment-provider integration and settlement testing, browser/mobile end-to-end flows, account-deletion behavior, cross-market authorization, incident/evidence workflows, backups, alerting and incident response. Staging email verification remains disabled because a verified sender/provider is not configured. Real payments should remain disabled until the payment adapter, provider-signature verification, idempotency, failure/replay/refund handling and reconciliation are tested.

## Safety principles

1. Keep staging and production credentials/data isolated.
2. Never commit .env files, keys, tokens, signing keys, database dumps or personal data.
3. Use synthetic test accounts/data only on staging URLs.
4. Do not enable real payments or email verification until provider credentials and end-to-end behavior have been verified.
5. Preserve strict UK/GBP and India/INR marketplace separation.
6. Do not force-push or reuse retired production infrastructure.
7. Treat staging as test-only; do not share sensitive or real customer data on it.

## Next step

Run browser and mobile smoke tests against the staging marketplace, focusing first on signup/login, UK and India separation, job posting/bidding, acceptance and status transitions, notifications, incident/evidence handling, and account deletion. Fix any findings and rerun [GitHub Validate](https://github.com/Post2Drive/post2drive-app/actions/workflows/validate.yml) before considering broader tester access.

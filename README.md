# Post2Drive

**Post2Drive Logistics Network** is a UK-first freight and courier marketplace project, with UK and India markets separated at the application and data-access layers.

## Repositories

- **Application source:** [Post2Drive/post2drive-app](https://github.com/Post2Drive/post2drive-app) — canonical app repository. The full source bundle still needs to be pushed; current main contains import/status docs only.
- **Project/profile:** this repository — overview, operating posture, and release notes. Do not duplicate the application code here.

## Railway staging

A private Railway project named **Post2Drive Staging** has been provisioned with persistent Postgres and Redis services, plus a configured web service.

Reserved test URL: https://post2drive-web-staging.up.railway.app

**The URL is not serving the app yet.** The web service has no source or deployment until the complete app is published to GitHub and CI passes. See [Staging and Release Status](docs/STAGING_AND_RELEASE_STATUS.md) for service IDs and next steps.

## Release posture

Post2Drive is in active development and is **not production-ready**.

- Targeted source contract tests pass for market isolation, timezone/DST handling, lifecycle guards, reliability calculations and the health endpoint contract.
- The complete dependency install, Prisma validation/migrations, TypeScript check and Next.js production build remain unverified.
- Real email delivery, payment-provider settlement, browser/mobile end-to-end flows, backups, alerting and incident response remain release gates.
- Redis is provisioned but not yet used by app code; do not claim performance gains until integrated and tested.

## Safety principles

1. Keep staging and production credentials/data isolated.
2. Never commit .env files, keys, tokens, signing keys, database dumps or personal data.
3. Use synthetic test accounts/data only on the staging URL.
4. Do not enable real payments or email verification until provider credentials and end-to-end behavior have been verified.
5. Preserve strict UK/GBP and India/INR marketplace separation.
6. Do not force-push or reuse retired production infrastructure.

## Immediate next step

Follow the source-import instructions in the app repository, push the complete source without force, confirm the Validate workflow passes, and connect the existing Railway web service to main in the staging environment only.

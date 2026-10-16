# Post2Drive

**Post2Drive Logistics Network** is a UK-first freight and courier marketplace project, with UK and India markets kept separate at the application and data-access layers.

## Repositories

- **Application source:** [Post2Drive/post2drive-app](https://github.com/Post2Drive/post2drive-app) — the canonical application repository. Its clean-start source bundle is being imported as the first code baseline.
- **Project/profile:** this repository — project overview and operating status only. Application code should not be duplicated here.

## Current release posture

Post2Drive is in active development. Do not represent it as production-ready or open unrestricted public registration yet.

- A new private Railway project, **Post2Drive Staging**, has been scaffolded for non-production validation.
- The staging environment has no services, database, public domain, or environment variables attached yet.
- Targeted market-isolation, UK/India timezone, and lifecycle contract tests have passed in the prepared source workspace.
- A full dependency install, Prisma migration validation, TypeScript check, and Next.js production build have not yet been verified successfully in this environment.
- Real email delivery, payment-provider events/settlement, browser/mobile end-to-end flows, monitoring, backups, and incident response remain launch gates.

## Safety principles

1. Keep staging and production credentials/data isolated.
2. Never commit .env files, keys, tokens, keystores, database dumps, or user data.
3. Do not connect Railway to an empty or unverified source baseline.
4. Do not enable real payment or email flows until the provider configuration and end-to-end checks pass.
5. Preserve strict UK/GBP and India/INR marketplace separation.
6. Do not force-push or reuse retired production infrastructure.

## Next steps

1. Publish the clean-start source bundle to the application repository.
2. Review the GitHub Actions validation results and fix any build, migration, or type errors.
3. Configure a dedicated staging database and staging-only secrets.
4. Connect Railway staging to the verified application branch and exercise browser/mobile flows.
5. Review the launch-readiness gates before considering any production deployment.

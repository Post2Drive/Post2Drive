# Post2Drive

**Post2Drive Logistics Network** is a UK-first freight and courier marketplace project, with UK and India markets kept separate at the application and data-access layers.

## Repositories

- **Application source:** [Post2Drive/post2drive-app](https://github.com/Post2Drive/post2drive-app) — the canonical application repository. It currently has bootstrap documentation only; the prepared application source bundle has not yet been pushed.
- **Project/profile:** this repository — overview, release posture and project-operating notes. Do not duplicate the full application source here.

## Current release posture

Post2Drive is in active development. Do not represent it as production-ready or open unrestricted public registration yet.

- A private Railway project, **Post2Drive Staging**, has been scaffolded for non-production validation.
- The staging environment has no services, database, public domain, or environment variables attached.
- Targeted market-isolation, UK/India timezone, lifecycle and reliability-budget checks pass in the prepared source workspace.
- A complete dependency install, Prisma migration validation, TypeScript check and Next.js production build have not yet been verified successfully.
- Real email delivery, payment-provider events and settlement, browser/mobile end-to-end flows, monitoring, backups and incident response remain launch gates.

## Safety principles

1. Keep staging and production credentials/data isolated.
2. Never commit .env files, keys, tokens, keystores, database dumps or user data.
3. Do not connect Railway to a documentation-only or unverified application source branch.
4. Do not enable real payment or email flows until provider configuration and end-to-end checks pass.
5. Preserve strict UK/GBP and India/INR marketplace separation.
6. Do not force-push or reuse retired production infrastructure.

## Next steps

1. Follow the import guide in the app repository to publish the prepared source bundle without force-pushing.
2. Review GitHub Actions validation results and resolve any build, migration or type errors.
3. Configure a dedicated staging PostgreSQL database and staging-only secrets.
4. Connect Railway staging to the verified application branch and test browser/mobile flows.
5. Review all launch-readiness gates before considering a production deployment.

See [Staging and Release Status](docs/STAGING_AND_RELEASE_STATUS.md) for the current inventory and release checklist.

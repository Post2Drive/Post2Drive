# Post2Drive repository and release status

**As of 16 October 2026**

## Repository roles

- [Post2Drive/post2drive-app](https://github.com/Post2Drive/post2drive-app) — canonical application source. At present, it holds import/status docs only; the full app source still needs a push from the prepared source ZIP.
- [Post2Drive/Post2Drive](https://github.com/Post2Drive/Post2Drive) — project overview and release-status documentation. Do not duplicate the full app source here.

## Railway

The private Railway project **Post2Drive Staging** exists with a dedicated staging environment, but it is currently an empty scaffold.

- Project ID: 074d55f7-6a58-4c46-86aa-a2c7b0079859
- Environment ID: 293eb264-dd1d-4eef-87ca-016943459edf
- Services/deployments/domains/volumes/buckets/variables: none

No application has been deployed, and no live or staging credentials have been configured here.

## Verified source checks

Targeted tests pass for market/currency isolation, UK/India timezone conversion and DST edge cases, lifecycle/route guards, and reliability-budget calculations. ZIP integrity and excluded-artifact checks pass. Full dependency installation, Prisma validation/migration execution, TypeScript and Next.js production build remain unverified due dependency-installation constraints in this environment.

## Next release gates

1. Publish the prepared app source into the existing post2drive-app clone; review staged files for secrets and local output.
2. Inspect the Validate GitHub Actions result and fix failures.
3. Create a dedicated staging PostgreSQL database and configure staging-only secrets.
4. Connect Railway only to the verified app repo/branch in the staging environment.
5. Exercise browser/mobile flows, authentication, data isolation, account deletion, file/evidence access, email, payments, backup/restore and monitoring before considering production.

Do not use production customer data or credentials in staging. Do not force-push, create a production service, or promote the app before its release gates pass.

# Operations plan — pilot readiness

## Daily operating cycle
1. Recruit and review load posters.
2. Check that job listings have complete route, vehicle, timing, cargo and payment-term information where applicable.
3. Monitor new and stale listings; remove or flag cancelled and misleading posts.
4. Support driver discovery, bids and poster responses.
5. Track accepted jobs, cancellations, completion evidence and disputes.
6. Review trust/safety reports and account access issues.
7. Reconcile access status and payments only in a properly configured provider-backed environment; no real payment launch until verified.
8. Review marketplace health and user feedback daily during the pilot.

## Owners and staffing
Named owners and working hours have not been provided. Before the pilot, assign one accountable person for poster onboarding/listing quality, one for user support/disputes, and one for technical incidents. One person may cover multiple roles at very small scale, but ownership must be explicit.

## Minimum SOPs to write and test
- Poster verification and job-quality checklist.
- Driver onboarding and eligibility/document review.
- Suspicious job, fraud and user-report handling.
- Cancellation, failed pickup, delivery dispute and proof-of-delivery handling.
- Access expiry, refund request and payment reconciliation (after provider integration).
- Incident response, rollback and data access.
- Account deletion, retention and privacy requests.

## Dependencies / unresolved
- Email verification delivery and token lifecycle need end-to-end tests before enabling.
- Payment provider is not selected/verified for live use; keep real payments disabled.
- Backups, restore drill, monitoring/alerting, incident ownership and rollback need evidence.
- UK eligibility, insurance and operator/document requirements need country-specific professional/legal review.
- India operating, tax and transport compliance must be reviewed separately.
- Database ownership and read-only operations-dashboard target remain release gates from the current project record.

## Risks
| Risk | Severity | Mitigation |
|---|---|---|
| Not enough relevant jobs | Critical | Poster-first acquisition, narrow geography, honest supply preview |
| Fake/stale job listings | High | Poster checks, listing expiry, reporting and moderation |
| Drivers pay but get no value | Critical | Avoid broad paid launch until pilot shows repeat value; clear terms |
| Payment or access-state errors | High | Provider-backed integration, idempotency and regression tests |
| Market/currency leakage | Critical | Separate market tests and server-side enforcement |
| Disputes or non-payment between parties | High | Display terms, clear evidence trail and dispute process |
| Support overload | Medium | Limited pilot cohort, explicit support owner and response targets |

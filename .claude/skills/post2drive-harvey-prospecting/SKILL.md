---
name: post2drive-harvey-prospecting
description: Research and qualify real Post2Drive prospects using a Harvey-style sales workflow, then prepare human-reviewed outreach. Use for prospect lists, account research, discovery campaigns, and sales experiments.
---

# Post2Drive Harvey-style prospecting

## Purpose

Help Post2Drive validate real demand and build a qualified prospect pipeline. This skill is a workflow guide; it does not install or execute the Harvey application by itself.

Upstream project: https://github.com/ethanplusai/harvey

## First principles

- Distinguish research from outreach. Browsing public business information and drafting messages does not authorize sending them.
- Start with a small, manual dry run using public business information. Record the source URL and date for every material claim.
- Never fabricate contact details, company needs, buying intent, job volume, relationships, or personalisation signals.
- Do not treat a recruitment page as proof a business wants a marketplace, nor a prospect score as a probability of conversion.
- Keep UK and India prospect lists, pricing, currencies, and compliance analysis separate.
- Do not use or request secrets in chat. Configure credentials locally only if the user explicitly chooses to install and operate an external tool.
- Never send messages, start an automated campaign, or enable follow-ups without explicit user approval of the exact recipients, content, channel, timing, and volume.
- Do not import prospects' sensitive personal data. Prefer relevant business-level details and publicly offered business contact channels.

## Post2Drive initial target

For the UK pilot, prioritise West Midlands transport businesses and independent courier/owner-drivers whose operating areas and vehicle types match real available jobs. Validate posters and drivers separately.

Useful poster signals:
- Publicly stated same-day, multi-drop, haulage, pallet, distribution, subcontracting, or overflow-capacity services.
- Evidence of operating in the selected launch area.
- Publicly stated fleet, service, or recruitment information relevant to the hypothesis.

Useful driver/supply signals:
- Public pages inviting self-employed couriers, owner-drivers, or subcontractors to apply.
- Relevant vehicle categories and geographic coverage.

Signals are reasons to investigate, not proof of intent to join Post2Drive.

## Workflow

1. Confirm market, region, target side (job posters, drivers, or both), prospect count, and whether this is research-only or an approved outreach campaign.
2. Define a narrow ideal customer profile and explicit disqualifiers before researching.
3. Find prospects through public company websites and reputable public sources. Store the exact URL, observed fact, observation date, and confidence.
4. Score each account with transparent criteria such as regional fit, service relevance, evidence strength, and potential use case. Keep score separate from buying intent.
5. Produce a concise qualification record: company, public website, region, target side, sourced signals, unresolved questions, fit rationale, and next step.
6. Draft personalised outreach that refers only to verified public facts and asks for discovery rather than assuming demand.
7. Review applicable privacy, direct-marketing, and platform rules before contact. For UK outreach, check current PECR/UK GDPR requirements for the recipient type; obtain qualified advice where uncertain.
8. Before any live sending, show the complete recipient list, exact message, sending method, daily volume, follow-up plan, opt-out handling, and compliance rationale. Wait for explicit approval.
9. After an approved campaign, log delivery, replies, opt-outs, objections, discovery calls, pilot commitments, and completed jobs. Suppress opt-outs immediately.

## Evidence standard

Separate:
- **Observed fact:** directly supported by a linked public source.
- **Inference:** a plausible interpretation of the fact.
- **Unknown:** not established by available evidence.

Do not invent email addresses or infer personal email formats. Use only contact channels that the business publishes or has expressly authorised. Do not claim prospects were contacted unless a real send is confirmed.

## Success metrics

Optimise for qualified discovery conversations, genuine job-posting commitments, suitable driver availability, accepted/completed jobs, repeat activity, and willingness to pay—not raw lead or signup counts.

## Safety boundary

A local installation of Harvey is a separate software setup and security decision. Review its current README, dependencies, isolation controls, outbound-email defaults, and data handling before use. Begin in dry-run mode. This skill alone must not launch the app, connect a mailbox, or send anything.

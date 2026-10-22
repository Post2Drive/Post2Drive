---
name: post2drive-mirofish-simulation
description: Design and evaluate MiroFish-style multi-agent market simulations for Post2Drive pricing, launch, trust, and two-sided marketplace liquidity. Use when comparing business hypotheses or preparing a simulation evidence pack.
---

# Post2Drive MiroFish market simulation

## Purpose

Use multi-agent simulation to generate hypotheses about Post2Drive's marketplace. This skill is a planning and analysis workflow; it does not itself execute the MiroFish engine.

Upstream project: https://github.com/666ghj/MiroFish

## Non-negotiable interpretation

- Clearly label whether work is (a) an in-chat qualitative simulation, (b) a real MiroFish engine run, or (c) real-world customer validation.
- Simulated agents are not real customers, a representative survey, evidence of demand, or a reliable conversion forecast.
- Never report invented agent counts, probabilities, experiment runs, or engine outputs as observed facts.
- Treat simulation outputs as hypotheses to test with interviews, landing-page experiments, real pilot listings, and completed jobs.
- Keep UK/GBP, India/INR, and any euro-market assumptions separate.
- Do not put credentials, access tokens, personal customer records, or confidential secrets into the simulation corpus.

## Default Post2Drive experiment

Unless the user specifies otherwise, define:
- Geography: a tightly bounded West Midlands pilot area.
- Sides: job posters and drivers modelled separately.
- Candidate offer: three months of free access, followed by clearly disclosed paid access.
- Comparators: 12 months free; a short paid trial; and the status quo (existing networks, WhatsApp/local groups, load boards, subcontracting networks).
- Primary question: which conditions make both sides repeatedly find enough relevant value to participate?

The three-month offer is a hypothesis, not a validated decision.

## Build the evidence pack

1. Gather current Post2Drive product facts, current UK pricing, onboarding flow, listing requirements, and known product limitations from repository sources.
2. Research competitors from public sources and cite URLs and dates. Mark missing or uncertain data rather than filling gaps.
3. Separate verified facts, assumptions, and open questions.
4. Define personas without pretending they are actual interviewed people. Include distinct needs for small transport businesses, courier operators, independent van drivers, owner-drivers, and small fleets where relevant.
5. Specify the decision the simulation should inform, candidate scenarios, observable outputs, and criteria that could falsify the preferred hypothesis.
6. Keep source material concise and relevant; do not feed unsupported claims into the graph as established truth.

## Scenario design

Run comparable scenarios with only the intended variable changed:
- Local concentration versus broad UK launch.
- Three months free versus 12 months free versus paid access from the outset.
- Posters-first versus driver-first acquisition.
- Verified, complete job listings versus sparse/low-quality listings.
- Different trust and verification levels.

Do not assume more agents or longer simulation automatically means more accurate results. If the real engine is used, record repository commit/version, configuration, model/provider, seed or run identifiers when available, inputs, errors, and output files. Verify current installation requirements in the upstream README before installing anything.

## Analyse outputs

For each scenario, report:
- Job-poster motivations, adoption triggers, objections, and alternatives.
- Driver motivations, adoption triggers, objections, and alternatives.
- Liquidity bottlenecks: suitable jobs, geography, timing, vehicle match, response rate, acceptance, completion, and repeat usage.
- Pricing and free-trial risks, including free-only users and willingness-to-pay uncertainty.
- Trust, verification, cancellation, payment-term, insurance, privacy, and dispute risks.
- Which conclusions are stable across scenarios and which depend heavily on assumptions.
- Confidence as a qualitative judgement, not a fabricated statistical probability.

Explicitly distinguish raw registrations from active users, matched jobs, completed jobs, repeat activity, and paid conversion.

## Convert simulation to validation

For every high-impact hypothesis, define a real-world test with:
- Target segment and sample/recruitment method.
- A neutral question or observable behaviour.
- Success and failure evidence.
- A time window and owner.
- The decision that would change based on the result.

For the initial pilot, interview job posters and drivers separately, seek genuine job-posting commitments, recruit drivers matched to those jobs, and track suitable responses, accepted/completed jobs, cancellations, repeat use, and willingness to pay.

## Safety and scope

Do not change Post2Drive application code, production/staging infrastructure, deployment settings, or live customer data as part of a simulation unless separately authorised. Do not install MiroFish, provision paid services, or send data to external providers without explicit user approval. Keep simulation artifacts in the business-research/profile repository, not the app runtime repository.

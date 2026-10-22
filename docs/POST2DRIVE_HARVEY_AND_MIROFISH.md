# Harvey and MiroFish workflows for Post2Drive

These are complementary business-research workflows, not app dependencies.

## Harvey: prospect research and outreach preparation

Skill: `.claude/skills/post2drive-harvey-prospecting/SKILL.md`

Upstream project: https://github.com/ethanplusai/harvey

Use it to research real transport businesses and publicly advertised driver opportunities, qualify prospects against a clear profile, and draft human-reviewed discovery outreach. Start with public information and a dry run. Never send email or run an automated campaign without explicit approval of recipients, content, volume, timing, and follow-up rules.

## MiroFish: market hypothesis simulation

Skill: `.claude/skills/post2drive-mirofish-simulation/SKILL.md`

Upstream project: https://github.com/666ghj/MiroFish

Use it to compare hypotheses about marketplace liquidity, launch concentration, pricing, trial duration, trust, and adoption. Always label qualitative in-chat work separately from an actual engine run. Simulated opinions do not establish real demand or conversion.

## Suggested combined workflow

1. Use MiroFish-style scenarios to identify the riskiest assumptions and the objections to test.
2. Use Harvey-style prospect research to identify real businesses and driver recruitment channels relevant to those assumptions.
3. Conduct discovery conversations and seek commitments to genuine pilot jobs.
4. Match a small cohort of suitable drivers to real listings.
5. Measure accepted and completed jobs, repeat usage, and willingness to pay.
6. Update the simulation with real evidence, keeping assumptions and observations clearly separated.

## Repository and operational boundaries

- This repository holds research workflows and guidance. These skill files do not install either upstream application.
- Do not add either tool as a runtime dependency of `post2drive-app`.
- Verify upstream installation, security, license, and service requirements before installing or running either project.
- Never commit secrets or personal customer data.
- No prospect should be contacted automatically merely because a skill was invoked.

# Founder skills for Post2Drive

This is an isolated copy of the 11 Claude skills from [Jakeschincariol/founder-skill](https://github.com/Jakeschincariol/founder-skill), pinned to upstream commit `fd9385b0cfe1b96bebce3898fbd506d73eff5a9d`.

The skills live under `.claude/skills/founder-*/` in this project/profile repository, not in `post2drive-app`. They are business-research tools, not app runtime code and are not deployed to Railway.

## Run order

`/founder-board` → `/founder-competitors` → `/founder-consumer --quick` → `/founder-pricing` → `/founder-offer` → `/founder-cfo` → `/founder-marketing` → `/founder-brand` → `/founder-ops` → `/founder-launch` → `/founder-plan`.

Start with the 20-buyer quick panel. Python 3.8+ is needed for the helper scripts; they use the standard library. The skills write research into a local `founder/` folder.

## Post2Drive guardrails

- Evaluate UK and India markets separately, including currency, customer acquisition, pricing, compliance and support.
- Buyer agents are simulated. Treat their buy rate as an optimistic ceiling, not a demand forecast. Validate with real drivers and businesses using interviews, waitlists, landing-page tests or paid pilots.
- Use real cost data where available; clearly label estimates and never infer profitability from missing inputs.
- Competitor research must cite public sources and must not invent prices, reviews or market facts.
- Review legal, tax, payments, driver eligibility and regulatory conclusions with qualified sources or professionals.
- Do not commit secrets or real customer personal data in research outputs.
- Do not copy these skills into `post2drive-app` or connect them to app runtime without a separate engineering decision.

## Upstream and license

Source: https://github.com/Jakeschincariol/founder-skill  
Pinned upstream: https://github.com/Jakeschincariol/founder-skill/commit/fd9385b0cfe1b96bebce3898fbd506d73eff5a9d  
MIT license and upstream copyright notice are preserved in `third_party/founder-skill/LICENSE`.

This is a copied snapshot, not an automatic sync. Review upstream updates before importing them.


## Additional market-research workflows

Two Post2Drive-specific workflows are included alongside the founder skills:

- `.claude/skills/post2drive-harvey-prospecting/SKILL.md` — prospect research, qualification, and human-reviewed outreach preparation using a Harvey-style workflow.
- `.claude/skills/post2drive-mirofish-simulation/SKILL.md` — structured market and multi-agent simulation planning using MiroFish-style scenarios.
- `docs/POST2DRIVE_HARVEY_AND_MIROFISH.md` — overview and suggested combined workflow.

These are local workflow instructions, not copies of either upstream application. They do not install or execute Harvey or MiroFish. Keep all prospect outreach human-approved, treat simulation outputs as hypotheses rather than demand evidence, and keep the skills in this research/profile repository rather than `post2drive-app`.

Upstream projects:
- Harvey: https://github.com/ethanplusai/harvey
- MiroFish: https://github.com/666ghj/MiroFish

Verify current upstream licenses, setup requirements, security controls, and provider costs before installing either application.

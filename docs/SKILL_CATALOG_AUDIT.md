# Skills and plugin catalog audit

**Review target:** `Post2Drive/Post2Drive`, branch `research/founder-skills-post2drive`  
**Review date:** 2026-10-23

## Scope checked

Fetched and inspected all 11 imported Founder skills:
- `founder-board`
- `founder-competitors`
- `founder-consumer`
- `founder-pricing`
- `founder-offer`
- `founder-cfo`
- `founder-marketing`
- `founder-brand`
- `founder-ops`
- `founder-launch`
- `founder-plan`

Fetched and inspected all three Post2Drive-specific skills:
- `post2drive-harvey-prospecting`
- `post2drive-query-router`

The available plugin skill catalogue returned 89 entries in this review. Major families represented include Railway, Windsor.ai, vidIQ, Figma, Shopify, Product Design, MagicPath, Notion, OpenAI artifact templates and routers, plugin management, and Superpowers engineering workflows. The connected tool inventory also includes GitHub, Canva, Automations, and Files. This is a routing inventory, not a requirement to invoke every skill for every request.

## Findings

### Founder skills

The 11 skills form a sensible business workflow from board review, competitor research and simulated buyer panel through pricing, offer, unit economics, marketing, brand, operations, launch and plan compilation. Their key limitation is that simulated buyer panels and derived purchase rates are not real customer evidence. The skills do contain warnings to label simulated results and validate with real buyers. Treat any outputs as hypotheses and check assumptions, price inputs and cited sources before making decisions.

### Harvey-style prospecting

The skill correctly separates public-source research from live outreach, requires sourced signals, forbids fabricated contacts and unapproved sending, and recommends tracking real commercial outcomes. The skill does not install Harvey or run its engine.

### Query router

The router's governing principle is correct: select the narrowest useful skill/tool set for the task rather than invoking every plugin. It routes core Post2Drive areas, documents, engineering, infrastructure, research, analytics and external actions. A runtime still has to load the skill files and have the relevant tools and account permissions available.

## Routing coverage to preserve

| Request type | Route |
|---|---|
| General answer or explanation | Answer directly; use web only when freshness or public sources matter |
| Current public facts or competitor research | Web research with citations |
| Private project or conversation files | Files tools and exact file references |
| GitHub source, branches, issues, PRs, CI | GitHub connector and engineering skills |
| App code, APIs, database, auth, security, tests | Canonical `Post2Drive/post2drive-app` plus applicable planning/debugging/TDD/review/verification skills |
| Railway, deploys, environments, variables, services | Railway skill first; read-only checks before changes; obey current deployment limits |
| UX audit, accessibility, user flows | Product Design audit/research; Figma when relevant |
| Figma edits, code context, diagrams, specs, files | Exact Figma skill; mandatory prerequisites before matching tools |
| Shopify store and commerce | Shopify skill/tools |
| Notion research, specs, trackers, meeting notes | Matching Notion skill/tools |
| Canva designs | Canva tools when an actual Canva artifact is intended |
| YouTube channel, retention, trends, packaging | The specific vidIQ skill matching the request |
| Connected marketing/commerce analytics | Windsor.ai when the required source is connected |
| Reminders, recurring summaries, conditional checks | Automations tools |
| Documents, spreadsheets, presentations, PDFs | Relevant artifact router/template when appropriate |
| Sales prospect research and outreach drafts | Harvey-style workflow; actual Harvey only after separate setup/approval |
| Pricing/launch/customer assumptions | Founder skills and MiroFish-style workflow; actual MiroFish only after separate setup/approval |
| Plugin discovery, connection, permissions | Plugin Management and current connection-status checks |
| Reusable skill creation/editing | Superpowers writing-skills guidance, then verify the file |
| Bug or failed test | Systematic debugging, then reproduce and test |
| New feature or behavior change | Brainstorming/planning, TDD and verification as appropriate |
| Code review / integration | Request/receive review and finishing-branch guidance; do not merge without approval |
| File creation | Correct artifact skill, then verify exact output path before sharing |

## Required safeguards

- Never ask the user to paste passwords, API tokens or private keys into chat.
- Never claim a plugin is connected because a skill exists; check live availability and permissions.
- Never claim an engine run, test, email send, deployment, or file creation without evidence.
- Never send/publish/buy/deploy/delete/merge or mutate infrastructure without explicit authorisation.
- Keep UK/GBP and India/INR assumptions separate.
- Do not put app runtime code in the profile/research repository.
- Preserve the distinction between source facts, inference, simulation, and real-world validation.
- For external research, cite current reliable sources; for private workspace facts, use the relevant connector/file source.

## Limitations and follow-up

This review confirms that the listed skill files exist on the branch and that their content has been inspected. It does not execute every skill end-to-end, install third-party applications, connect every plugin, test every provider, or verify that all agent runtimes automatically discover `.claude/skills`. Those checks are environment-specific and should be done when a particular workflow is first used.

The correct operating model is **coverage plus selective routing**, not running all 89 plugin skills for each query.

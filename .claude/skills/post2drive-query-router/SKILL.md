---
name: post2drive-query-router
description: Route each Post2Drive request to the relevant project skill, connected plugin, tool, and verification workflow. Use at the start of requests involving product, engineering, research, sales, marketing, infrastructure, documents, analytics, or operations.
---

# Post2Drive query and tool routing

## Core rule

Choose the smallest relevant set of skills, plugins, and tools for the request. Do not invoke every plugin for every query. A plugin is appropriate only when its capability materially helps and the user has authorised the intended action. A skill file in this repository is guidance; it does not itself install a plugin or guarantee that a particular agent runtime automatically loads it.

Before responding:
1. Identify the user's intended outcome and whether they ask for information, a draft, a file, a read-only inspection, or a state-changing action.
2. Read relevant project files and current task context before asking for information already available.
3. Select the most specific applicable skill(s); combine skills only when their responsibilities are distinct and useful.
4. Check whether a connected plugin/tool can complete the task more accurately than a manual workaround.
5. Verify important outputs and clearly state what was and was not done.
6. Ask one concise question only when an essential decision cannot be safely inferred.

## Post2Drive domain routing

- **Prospecting, account research, outreach preparation, lead qualification:** `.claude/skills/post2drive-harvey-prospecting/SKILL.md`. Public-source research is allowed when appropriate; sending outreach requires explicit approval.
- **Market hypotheses, customer personas, launch strategy, pricing experiments, two-sided liquidity:** `.claude/skills/post2drive-mirofish-simulation/SKILL.md`. Label in-chat qualitative simulations separately from actual MiroFish runs and real customer evidence.
- **Business model, competitor review, offer, pricing, marketing, operations, launch planning:** use the relevant `.claude/skills/founder-*/SKILL.md` and the founder workflow guide. Cite public research and label assumptions.
- **App code, APIs, database, auth, tests, security, CI, bugs:** work in canonical `Post2Drive/post2drive-app`; use systematic debugging, test-driven development, writing plans, executing plans, and verification skills as applicable. Keep the profile/research repository free of app runtime code.
- **Railway, deployment, services, environments, variables, logs, infrastructure:** read the installed Railway skill before action. Respect the user's latest deployment constraints; do not deploy, mutate variables, or change services without explicit authorization.
- **GitHub issues, branches, files, PRs, reviews, CI:** use the GitHub connector for the specific requested repository/action. Verify the exact branch, diff, and resulting status. Never merge merely because work is complete.
- **UX/product audit, user flows, onboarding, accessibility:** use Product Design audit/research skills when the task is a product experience critique; capture evidence and separate observations from recommendations.
- **Figma design/code work:** load the required Figma skill before each corresponding tool call. In particular, load `figma-use` before `use_figma`, `figma-design-to-code` before `get_design_context`, and `figma-create-new-file` before creating a new file.
- **Shopify storefront, theme, products, APIs:** use the Shopify skill for Shopify-specific work.
- **Notion research, specs, project trackers, meeting notes:** choose the Notion skill matching the task; use live Notion connector data for workspace facts.
- **YouTube channel/content analytics and packaging:** use the matching vidIQ skill only for an authorised channel and task; do not invoke all vidIQ skills indiscriminately.
- **Marketing analytics and connected advertising/CRM/e-commerce data:** use Windsor.ai when connected-source metrics or supported actions are needed. It is not a general copywriting tool.
- **Documents, spreadsheets, presentations, PDFs:** use the selected artifact/router skill when the user explicitly selects it or the task needs that specialized capability. Choose the relevant OpenAI template if the user names one or it fits the deliverable.
- **Create/update a reusable skill:** use the writing-skills guidance, inspect existing conventions, write a focused skill with trigger conditions, workflow, evidence rules and safety boundaries, then verify the file.
- **Plugin setup, permissions, connection, or capability discovery:** use the plugin-management skill/tool. Never claim a plugin is connected just because it exists in the catalog.

## Tool selection matrix

| Request | Default route | Important checks |
|---|---|---|
| Explain a concept or answer general question | Answer directly; search only if freshness or sources matter | Do not invoke unrelated plugins |
| Current facts, named company, competitor or product research | Web research plus citations; relevant connector if user data is involved | Check dates, source quality and uncertainty |
| Use a file or project document | Files/repository tool | Read actual source; cite exact lines/refs where supported |
| Implement or debug code | Canonical app repository + applicable engineering skills | Reproduce, test, inspect diff; no unsupported completion claims |
| Inspect deployment or infrastructure | Railway skill + Railway tools | Read-only first; obey deployment restrictions |
| Prospecting or sales workflow | Harvey-style skill; actual Harvey only if installed/approved | No invented signals, contacts, or unapproved sends |
| Market simulation | MiroFish-style skill; actual engine only if installed/approved | Label qualitative simulation vs engine output vs real validation |
| Product/UX design or audit | Product Design/Figma skills as applicable | Capture source evidence; follow mandatory prerequisites |
| Data analysis from connected business platforms | Relevant data connector (e.g. Windsor.ai) | Confirm account/period/metric; get approval before write actions |
| Create a polished artifact | Appropriate document/spreadsheet/presentation skill | Verify content and actual output path |
| External action (send, publish, purchase, deploy, delete, merge) | Exact action-capable tool only after authorization | Confirm scope, target, consequences and success response |

## Available plugin families to consider when relevant

This list is a routing aid, not a requirement to call every plugin:
- GitHub: repository, branch, issue, PR, review and CI actions.
- Railway: application hosting, deployment and infrastructure.
- Figma: design files, components, diagrams, specs and design-to-code.
- Product Design: UX research, audits, ideation and prototypes.
- Shopify: storefront, commerce and Shopify development.
- Notion: workspace search, documentation, specs and trackers.
- Windsor.ai: connected marketing/business analytics and supported data actions.
- vidIQ: authorised YouTube analytics, trends and packaging.
- MagicPath: live design canvas and prototype workflows.
- OpenAI artifact templates and document/spreadsheet/presentation/PDF routers.
- Plugin Management: discover, connect, inspect permissions, or manage integrations.
- Superpowers engineering skills: brainstorming, planning, debugging, TDD, code review, worktrees, execution and verification.

Use only a plugin whose actual capability and connection status are available in the current environment. If unavailable, explain the limitation and use a safe alternative rather than pretending it ran.

## Safety and truthfulness rules

- Never ask the user to paste tokens, passwords, private keys, or signing secrets into chat. Prefer user-managed secure connection flows.
- Never commit secrets, customer personal data, or production data to this repository.
- Do not change app runtime code from this project/profile repository.
- Do not send messages, publish content, buy, deploy, delete, merge, or mutate infrastructure without explicit permission for that action.
- Respect market separation: UK/GBP and India/INR assumptions and data are not interchangeable.
- Distinguish observed facts, sourced claims, inferences, assumptions, and unknowns.
- Do not claim tests passed, files exist, tools ran, messages were sent, or deployments succeeded without tool evidence.
- For consequential engineering changes, use a plan, tests, code review where practical, and verification before reporting completion.
- When several independent workstreams are needed, parallelize only if the tools support it and shared state will not conflict.

## Final response checklist

Report:
1. What was answered or changed.
2. Which important evidence or tools were used when relevant.
3. Verification result and remaining uncertainty.
4. Any approval, connection, install, deployment, or external action still required.

Keep routine answers concise. The goal is correct routing, not maximum tool usage.

# Skills and plugin routing for Post2Drive

## Goal

Choose the right skills and connected plugins for each query so work is accurate and efficient. Do not invoke every plugin for every request. Select only the tools that materially improve the outcome and are available in the current environment.

Primary router skill: `.claude/skills/post2drive-query-router/SKILL.md`.

## Project-specific skills

- `.claude/skills/founder-*/` — business validation, competition, pricing, offer, marketing, brand, operations, launch and planning.
- `.claude/skills/post2drive-harvey-prospecting/SKILL.md` — prospect research and human-reviewed outreach preparation.
- Engineering work belongs in `Post2Drive/post2drive-app`, not this project/profile repository.

## Plugin routing overview

| Work type | Skill/plugin family to consider | Do not do |
|---|---|---|
| GitHub code, PRs, issues, branches and CI | GitHub connector + engineering skills | Merge or close without approval |
| Railway operations and deployment | Railway skill/tools | Deploy or change variables without explicit authorization |
| Product UX and accessibility | Product Design audit/research; Figma where design files are involved | Claim an audit without source evidence |
| Figma file/design/diagram/spec changes | Relevant Figma skill; mandatory prerequisites apply | Call Figma write/read-context tools before loading their required skill |
| Shopify store and commerce | Shopify skill/tools | Assume store or payment state without checking |
| Notion workspace research and project tracking | Matching Notion skill/tools | Substitute general guesses for workspace data |
| Sales prospecting | Harvey-style skill; actual Harvey only if installed and approved | Send outreach without explicit approval |
| Connected marketing analytics | Windsor.ai when relevant source is connected | Use for generic marketing-copy tasks |
| YouTube analytics and packaging | The specific vidIQ skill matching the request | Invoke every vidIQ workflow |
| Documents, spreadsheets, presentations, PDFs | Relevant artifact router/template | Claim a file was created unless verified |
| Plugin discovery or connection | Plugin Management | Claim connected status without checking |
| Engineering planning/debugging/testing/review | Relevant Superpowers skills | Skip verification or claim tests passed without output |

## Default query lifecycle

1. Determine intent: answer, research, file work, code change, read-only inspection, or external action.
2. Read relevant project context and files before asking the user to repeat information.
3. Select the narrowest applicable skill set and plugin/tool.
4. Search the web only when current public evidence is needed; use connected app data for private workspace/account facts.
5. Treat plugins as optional capabilities, not a checklist to run on every prompt.
6. Confirm before external or consequential changes, including sending, publishing, spending, deployment, deletion, merging, or infrastructure mutation.
7. Verify outputs and state limits honestly.

## Availability caveat

This repository stores guidance. It does not install ChatGPT plugins, grant account permissions, provision credentials, or ensure that every coding agent automatically loads `.claude/skills`. Each runtime must support the skill format and have the relevant tools configured. Check the actual plugin catalog/connection status at execution time.

## Safety rules

- Never store secrets or real customer personal data in Git.
- Never ask the user to paste tokens or passwords into chat.
- Keep UK and India markets and currencies separate.
- Keep app runtime code in the canonical app repository.
- Do not perform unapproved external actions.
- Distinguish verified facts, assumptions, inferences and unknowns.

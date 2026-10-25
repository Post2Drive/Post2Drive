# Upstream provenance

This directory vendors Cloudflare's public `security-audit` skill.

- Upstream repository: https://github.com/cloudflare/security-audit-skill
- Upstream skill directory: https://github.com/cloudflare/security-audit-skill/tree/main/skills/security-audit
- License: MIT; see https://github.com/cloudflare/security-audit-skill/blob/main/LICENSE
- See the upstream README for installation, runtime requirements, and supported agent platforms.

Review upstream changes before updating this copy. This is a vendored copy, not an independently maintained fork.

## Safety

The workflow requires an OS-enforced sandbox before running target-controlled builds, tests, browsers, or other processes. If the required isolation controls cannot be enforced, do not execute target code. Adding the skill does not run an audit, authorize live testing, merge code, or deploy anything.

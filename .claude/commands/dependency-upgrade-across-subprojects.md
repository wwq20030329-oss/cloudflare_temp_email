---
name: dependency-upgrade-across-subprojects
description: Workflow command scaffold for dependency-upgrade-across-subprojects in cloudflare_temp_email.
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /dependency-upgrade-across-subprojects

Use this workflow when working on **dependency-upgrade-across-subprojects** in `cloudflare_temp_email`.

## Goal

Upgrade dependencies in one or more subprojects (frontend, worker, smtp_proxy_server, etc.), often for security, compatibility, or feature reasons.

## Common Files

- `frontend/package.json`
- `frontend/pnpm-lock.yaml`
- `worker/package.json`
- `worker/pnpm-lock.yaml`
- `vitepress-docs/package.json`
- `vitepress-docs/pnpm-lock.yaml`

## Suggested Sequence

1. Understand the current state and failure mode before editing.
2. Make the smallest coherent change that satisfies the workflow goal.
3. Run the most relevant verification for touched files.
4. Summarize what changed and what still needs review.

## Typical Commit Signals

- Update dependency versions in package.json or requirements.txt
- Update lock files (pnpm-lock.yaml, package-lock.json)
- Update Dockerfile or related CI files if needed
- Commit with chore(deps): or chore: upgrade dependencies message

## Notes

- Treat this as a scaffold, not a hard-coded script.
- Update the command if the workflow evolves materially.
Status: Shipped
Owner: Architect
Date created: 2026-07-26
Last updated: 2026-07-26
Date shipped: 2026-07-26
Date archived: 2026-07-26
Linear issue:
Linear project:
GitHub repository:
Last Linear sync:
Primary decision channel: Chat session 2026-07-26

# Define Delegation and Context Isolation Policy

## Goal (required)

Make role delegation predictable and reduce the risk of requirements or
context from separate tasks being mixed during AI-assisted work.

## Scope (required)

- Document when subagents or role-based delegation may be used.
- Define the minimum handoff packet for delegated work.
- Define ownership and concurrency rules for repository files.
- Define how delegated work reports changes, validation, and deviations.
- Define the final integration responsibility.

## Non-goals (required)

- Add an agent orchestration tool.
- Require multiple agents for every task.
- Create separate repositories or worktrees.
- Change RTL, testbench, or hardware architecture.
- Guarantee context isolation that the execution environment does not provide.

## Accepted Owner Decisions (required)

- 2026-07-26 — Role selection and subagent delegation must follow explicit
  task triage. (source: chat session 2026-07-26)
- 2026-07-26 — Delegated work must use a bounded handoff packet and must not
  rely on unrelated conversation context. (source: chat session 2026-07-26)
- 2026-07-26 — The primary agent remains responsible for final integration and
  validation of the working tree. (source: chat session 2026-07-26)

## Canonical Docs (optional — remove if not applicable)

- [`AGENTS.md`](../../AGENTS.md)
- [`docs/PLAN_TEMPLATE.md`](../PLAN_TEMPLATE.md)

## Current State / Code Facts (optional — remove if not applicable)

- Repository roles are documented under `.ai/roles/`.
- The repository does not define an automatic subagent orchestration mechanism.
- The active agent must therefore apply the same handoff discipline manually
  when independent delegation is unavailable.

## Proposed Direction (required)

Add a repository-wide delegation policy to `AGENTS.md`. The policy will state
that triage precedes delegation, delegated tasks receive only the relevant
plan and bounded context, file ownership must not overlap, and final review is
performed against the actual working tree.

## Files Likely Touched (optional — remove if not applicable)

- `AGENTS.md`
- `docs/design/2026-07-26-delegation-context-isolation.md`

## Testing / Validation Strategy (optional — remove if not applicable)

- Run `git diff --check`.
- Confirm the policy names triage, handoff scope, file ownership, reporting,
  and final integration responsibilities.
- Confirm no implementation files are changed.

## Acceptance Criteria (required)

- `AGENTS.md` documents when delegation occurs.
- `AGENTS.md` defines a bounded handoff packet.
- `AGENTS.md` prohibits overlapping concurrent ownership of files.
- `AGENTS.md` requires validation and deviation reporting.
- `AGENTS.md` assigns final integration responsibility to the primary agent.
- No unrelated repository files are changed.

## Open Questions (optional — remove if not applicable)

None.

## Immediate Next Tasks (required)

- Apply the policy during future task triage.
- Revisit the policy if the repository adopts an agent orchestration tool.

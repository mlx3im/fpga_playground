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

# Establish Git Commit Convention

## Goal (required)

Make commits consistent, readable, and easy to parse for humans and future
automation.

## Scope (required)

- Document a lightweight Conventional Commits-style format.
- Add a tracked commit-message template.
- Ignore macOS `.DS_Store` metadata.

## Non-goals (required)

- Enforce commits with hooks or CI.
- Rewrite existing commit history.
- Add commitlint or other external tooling.

## Accepted Owner Decisions (required)

- 2026-07-26 — Use a lightweight Conventional Commits-style convention with
  repository-specific types and scopes. (source: chat session 2026-07-26)
- 2026-07-26 — Add `.DS_Store` to `.gitignore`. (source: chat session 2026-07-26)

## Canonical Docs (optional — remove if not applicable)

- [`AGENTS.md`](../../../AGENTS.md)
- [`docs/PLAN_TEMPLATE.md`](../../PLAN_TEMPLATE.md)
- [`docs/DECISIONS.md`](../../DECISIONS.md)

## Current State / Code Facts (optional — remove if not applicable)

- The repository has no existing `.gitignore` or commit-message template.
- Existing commit messages are not governed by a documented convention.

## Proposed Direction (required)

Document `<type>(<scope>): <imperative summary>` in `AGENTS.md` and provide
`.gitmessage` with the supported types, scopes, and examples.

## Files Likely Touched (optional — remove if not applicable)

- `.gitignore`
- `.gitmessage`
- `AGENTS.md`
- `docs/design/2026-07-26-git-commit-convention.md`

## Testing / Validation Strategy (optional — remove if not applicable)

- Run `git diff --check`.
- Confirm `.DS_Store` is ignored with `git check-ignore -v .DS_Store`.

## Acceptance Criteria (required)

- `AGENTS.md` documents the commit format, types, scopes, and examples.
- `.gitmessage` is suitable for `git config commit.template`.
- `.DS_Store` is ignored at any repository level.
- No existing history is rewritten.

## Open Questions (optional — remove if not applicable)

None.

## Immediate Next Tasks (required)

- Configure local Git clients to use `.gitmessage` when desired.
- Consider commitlint or hooks only after the project has enough contributors
  to justify enforcement.

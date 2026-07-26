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

# Add Documentation Link Validation

## Goal (required)

Prevent broken local Markdown links, especially when plans move from
`docs/design/` to `docs/design/archive/`.

## Scope (required)

- Add an archive checklist to the plan workflow.
- Add a dependency-free local Markdown link checker.
- Repair existing broken archived-plan links.
- Document how to run the checker.

## Non-goals (required)

- Validate external URLs or network availability.
- Introduce a documentation framework or package dependency.
- Add CI configuration before the project has a CI baseline.
- Change RTL, board constraints, or hardware tooling.

## Accepted Owner Decisions (required)

- 2026-07-26 — Markdown links must be validated after a plan is moved to the
  archive directory. (source: chat session 2026-07-26)
- 2026-07-26 — Use a repository-local, dependency-free checker so validation
  works before a broader toolchain is selected. (source: chat session
  2026-07-26)

## Canonical Docs (optional — remove if not applicable)

- [`docs/PLAN_TEMPLATE.md`](../../PLAN_TEMPLATE.md)
- [`tools/check-doc-links`](../../../tools/check-doc-links)

## Current State / Code Facts (optional — remove if not applicable)

- Archived plans previously contained relative links that were valid before
  the move but broken after the move.
- The repository has no existing documentation link checker.

## Proposed Direction (required)

Add `tools/check-doc-links`, which scans local Markdown files, resolves local
relative links from each source file, and reports missing targets. External
URLs and fragment-only links are outside its scope. The plan template will
require link validation as part of archiving.

## Files Likely Touched (optional — remove if not applicable)

- `docs/PLAN_TEMPLATE.md`
- `tools/check-doc-links`
- `docs/design/archive/2026-07-26-git-commit-convention.md`
- `docs/design/archive/2026-07-26-delegation-context-isolation.md`
- `README.md`
- `docs/design/2026-07-26-documentation-link-validation.md`

## Testing / Validation Strategy (optional — remove if not applicable)

- Run `tools/check-doc-links` from the repository root.
- Run `git diff --check`.
- Confirm the checker detects a deliberately missing local target in a temporary
  fixture, if implementation testing requires it.
- Confirm no external URL is treated as a local failure.

## Acceptance Criteria (required)

- The plan template includes an explicit archive link-validation checklist.
- `tools/check-doc-links` runs without third-party dependencies.
- Existing Markdown links pass the checker.
- The checker reports the source file and target for failures.
- The checker does not modify repository files.
- The checker usage is discoverable from project documentation.

## Open Questions (optional — remove if not applicable)

- Should the checker become a CI gate when CI is introduced?
- Should heading-fragment validation be added in a later tooling task?

## Immediate Next Tasks (required)

- Run the checker before documentation commits.
- Revisit CI integration when a CI baseline is introduced.

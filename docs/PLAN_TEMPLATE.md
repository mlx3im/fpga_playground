<!-- Copy to docs/design/YYYY-MM-DD-<slug>.md for a new active plan. -->
<!-- Archive when shipped/paused: docs/design/archive/YYYY-MM-DD-<slug>.md -->
Status: Active | Shipped | Paused | Superseded
Owner:
Date created: YYYY-MM-DD
Last updated: YYYY-MM-DD
Date shipped: YYYY-MM-DD
Date archived: YYYY-MM-DD
Primary decision channel:

## How to use this template

1. Copy this file to `docs/design/YYYY-MM-DD-<slug>.md`.
2. Set the owner, lifecycle status, dates, scope, non-goals, and accepted
   decisions before implementation begins.
3. Keep the plan updated with validation evidence, deviations, open questions,
   and immediate next tasks.
4. Use the review packet sections for formal planning or post-implementation
   review.
5. Move the completed or paused plan to
   `docs/design/archive/YYYY-MM-DD-<slug>.md` and update its status and archive
   date.
6. After moving a plan, repair its relative links and run
   [`tools/check-doc-links`](../tools/check-doc-links) from the repository root.

## External Tracking (optional)

Linear issue:
Linear project:
GitHub repository:
Last Linear sync:

Plans are the working source of truth for task scope and decisions. Durable
cross-task decisions belong in [`docs/DECISIONS.md`](DECISIONS.md); plan-local
decisions remain in the plan.

# <Plan Title>

## Goal (required)

Plan-local decisions are listed below. Durable decisions are recorded in
[`docs/DECISIONS.md`](DECISIONS.md).

## Scope (required)

## Non-goals (required)

## Accepted Owner Decisions (required)

- YYYY-MM-DD — <decision>. (source: Linear issue TWI-123, Linear comment TWI-123#c45, chat session YYYY-MM-DD, PR #N, or file reference)

## Canonical Docs (optional — remove if not applicable)

## Current State / Code Facts (optional — remove if not applicable)

## Proposed Direction (required)

## Files Likely Touched (optional — remove if not applicable)

## Safety / Privacy / License Gates (optional — remove if not applicable)

## Testing / Validation Strategy (optional — remove if not applicable)

## Acceptance Criteria (required)

## Open Questions (optional — remove if not applicable)

## Immediate Next Tasks (required)

When archiving a plan, complete this checklist before marking the work done:

- update the lifecycle metadata
- move the plan to `docs/design/archive/`
- repair relative links from the archived location
- run `tools/check-doc-links`
- record the validation result in the plan

## Review Packets (optional — remove if not applicable)

### Review Packet Round N

Review type: Planning | Post-Implementation

#### Goal

#### Subject

Planning: plan/proposal to review.
Post-Implementation: implemented diff, commit status, and shipped scope.

#### Canonical Docs

#### Accepted Owner Decisions

#### Known Accepted Risks

#### Non-goals

#### Changes Since Last Round

#### Validation Evidence

Required for Post-Implementation. Optional for Planning.

#### Runtime / Browser / Package Versions

Required for Post-Implementation when tooling/browser/package behavior matters.

#### Deviations From Plan

Required for Post-Implementation.

#### Explicit Non-Coverage

Required for Post-Implementation. Optional for Planning.

#### Deferred Risks

#### Review Questions

#### Expected Output

Return findings as HIGH/MEDIUM/LOW. Answer each review question directly.

### Review Round N Triage

| Finding | Severity | Decision | Owner decision needed | Plan action |
| --- | --- | --- | --- | --- |

Rejected:

Deferred:

Outstanding owner decisions:

Review loop decision:

### Review Round N Conclusion

One paragraph: what was found or decided, what was fixed or deferred, whether another round is needed, and whether the plan is ready for the next lifecycle step.

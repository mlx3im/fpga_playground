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

# Establish Tang Nano 9K Project Foundation

## Goal (required)

Define the initial project architecture around the available Sipeed Tang Nano
9K board without beginning RTL implementation or committing to a complete
build toolchain.

## Scope (required)

- Establish the Tang Nano 9K as the primary hardware target.
- Define the boundary between board-independent RTL and board integration.
- Document the initial repository structure for board-aware development.
- Record known board facts and unresolved toolchain decisions.
- Add architecture and board reference documentation.

## Non-goals (required)

- Implement RTL or testbenches.
- Add Gowin project files, constraints, or build scripts.
- Select a final simulator, synthesis flow, or programming utility.
- Support additional FPGA boards.
- Define a complete application or hardware feature roadmap.

## Accepted Owner Decisions (required)

- 2026-07-26 — The Tang Nano 9K is the primary and initially only supported
  hardware target. (source: chat session 2026-07-26)
- 2026-07-26 — Reusable RTL must remain separate from Tang Nano 9K board
  integration. (source: chat session 2026-07-26)
- 2026-07-26 — Board-specific implementation and toolchain work is deferred
  until the architecture foundation is documented. (source: chat session
  2026-07-26)

## Canonical Docs (optional — remove if not applicable)

- [`docs/ARCHITECTURE.md`](../../ARCHITECTURE.md)
- [`docs/boards/tang-nano-9k.md`](../../boards/tang-nano-9k.md)
- [`docs/DECISIONS.md`](../../DECISIONS.md)
- [`AGENTS.md`](../../../AGENTS.md)

## Current State / Code Facts (optional — remove if not applicable)

- The repository contains documentation and empty implementation directories,
  but no RTL, testbench, constraints, or build configuration.
- The available board is a Sipeed Tang Nano 9K based on the Gowin
  GW1NR-LV9QN88PC6/I5 device.

## Proposed Direction (required)

Use a three-layer structure:

1. Board-independent synthesizable RTL under `rtl/core/`.
2. Tang Nano 9K wrappers and top-level integration under
   `rtl/board/tang_nano_9k/`.
3. Board constraints and tooling in dedicated `constraints/` and `tools/`
   locations.

Document the board’s clock, visible I/O, FPGA resources, and future integration
requirements without creating implementation files yet. Use the official
Gowin flow as the initial reference for future hardware builds; evaluate an
open-source flow separately after a first reproducible design exists.

## Files Likely Touched (optional — remove if not applicable)

- `docs/ARCHITECTURE.md`
- `docs/boards/tang-nano-9k.md`
- `docs/DECISIONS.md`
- `docs/design/2026-07-26-tang-nano-9k-foundation.md`

## Testing / Validation Strategy (optional — remove if not applicable)

- Confirm documentation links and paths are correct.
- Confirm the proposed structure does not require implementation directories
  that are outside the documented scope.
- Review board facts against the Sipeed and Gowin documentation.
- Run `git diff --check`.

## Acceptance Criteria (required)

- The primary hardware target is explicitly documented as Tang Nano 9K.
- The boundary between reusable RTL and board integration is explicit.
- Board facts, assumptions, and unresolved decisions are documented.
- The architecture does not imply that RTL or toolchain implementation has
  already begun.
- A durable board-target decision is recorded in `docs/DECISIONS.md`.

## Open Questions (optional — remove if not applicable)

- Should the first hardware build use Gowin EDA only, or also support an
  open-source flow?
- Which simulator should be the project validation baseline?
- Which board interfaces should be prioritized after the basic LED/button
  workflow?
- Should board constraints live at repository root or under a board-specific
  directory once implementation begins?

## Immediate Next Tasks (required)

- Select the initial simulation and hardware build tools in a follow-up plan.
- Create the first Tang Nano 9K build plan before adding constraints or RTL.

## Review Packets

### Review Packet Round 1

Review type: Post-Implementation

#### Goal

Confirm that the Tang Nano 9K project foundation is documented, bounded, and
ready to serve as the basis for a future tooling-selection plan.

#### Subject

The documentation changes committed in the Tang Nano 9K project foundation.

#### Canonical Docs

- [`docs/ARCHITECTURE.md`](../../ARCHITECTURE.md)
- [`docs/boards/tang-nano-9k.md`](../../boards/tang-nano-9k.md)
- [`docs/DECISIONS.md`](../../DECISIONS.md)
- [`AGENTS.md`](../../../AGENTS.md)

#### Accepted Owner Decisions

- The Tang Nano 9K is the primary and initially only supported hardware target.
- Reusable RTL remains separate from board integration.
- RTL, constraints, and toolchain implementation are deferred to later plans.

#### Known Accepted Risks

- The simulator, synthesis flow, programming utility, and first hardware
  demonstration remain open decisions.
- `AGENTS.md` does not yet list `constraints/`; this is deferred until the
  first board-build plan and does not block the documentation foundation.

#### Non-goals

- RTL, testbench, constraints, build scripts, and board implementation.
- Support for additional FPGA boards.

#### Changes Since Last Round

This is the first review round. The plan lifecycle was completed, the plan was
prepared for archival, and the durable decision link was updated for the
archived location.

#### Validation Evidence

- Documentation link checker passed for 15 Markdown files.
- `git diff --check` passed for the foundation lifecycle update.
- The repository contains no RTL, testbench, constraints, or build changes
  from this plan.
- An independent Reviewer inspected the current repository and confirmed the
  core board-target and RTL-boundary decisions.

#### Runtime / Browser / Package Versions

Not applicable. This plan changes documentation only.

#### Deviations From Plan

None for the shipped scope. Reviewer follow-ups are recorded as accepted
deferred risks above.

#### Explicit Non-Coverage

Toolchain selection, simulator selection, pin constraints, and hardware
validation are intentionally not covered.

#### Deferred Risks

- `constraints/` should be added to the repository-wide layout documentation
  before the first board-build plan.
- Toolchain choices may affect the eventual directory and validation commands.

#### Review Questions

- Is the Tang Nano 9K target explicit? Yes.
- Is reusable RTL separated from board integration? Yes.
- Does the foundation avoid implying that implementation has begun? Yes.
- Are deferred toolchain and hardware decisions visible? Yes.

#### Expected Output

Approve the foundation for archival and defer tooling and board-build decisions
to a follow-up plan.

### Review Round 1 Triage

| Finding | Severity | Decision | Owner decision needed | Plan action |
| --- | --- | --- | --- | --- |
| Foundation plan remained Active after implementation | HIGH | Fixed | No | Marked Shipped and archived |
| Archived-plan links were broken | MEDIUM | Fixed | No | Repaired and validated in `04ca1c3` |
| `constraints/` missing from `AGENTS.md` layout | MEDIUM | Deferred | Yes, before board-build work | Track in next repository-structure task |
| Blank external-tracking fields | LOW | Deferred | No | Revisit during plan-template maintenance |
| Architect role numbering typo | LOW | Deferred | No | Revisit during role-documentation maintenance |

Rejected:

None.

Deferred:

The `constraints/` layout update and low-priority documentation cleanup remain
outside this plan’s shipped scope.

Outstanding owner decisions:

Select the simulator and hardware build flow in a follow-up plan.

Review loop decision:

The HIGH finding is fixed, the broken-link finding is fixed, and the remaining
findings are explicitly deferred. The plan is ready for archival.

### Review Round 1 Conclusion

The foundation review confirmed that the Tang Nano 9K target, reusable RTL
boundary, and deferred implementation scope are clearly documented. The plan
lifecycle issue was corrected, archived links were repaired and validated, and
the remaining repository-layout and editorial items were explicitly deferred.
No further review round is required for this foundation plan.

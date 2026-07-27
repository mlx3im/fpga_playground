# AI Agent Guide

Repository-wide instructions for every AI agent working on FPGA Playground.
Role charters are under [`.ai/roles/`](.ai/roles/) and extend these rules.

## Session Start

Before the first action in a session:

1. Read this file.
2. Read [`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md) and
   [`docs/DECISIONS.md`](docs/DECISIONS.md).
3. Check `docs/design/` for an active plan. If the task changes architecture,
   RTL, verification, tooling, or documentation and no active plan exists, the
   Architect creates one from
   [`docs/PLAN_TEMPLATE.md`](docs/PLAN_TEMPLATE.md) before any file changes.
4. Read the charter for the role you will act in — see [Roles](#roles).

## Project Overview

An educational FPGA project. The goal is learning AI-assisted engineering while
developing FPGA designs. The project values maintainability, documentation, and
engineering practice over implementation speed.

## Current State

As of 2026-07-27 the repository is documentation-only. Update this section when
that changes.

- No RTL, testbenches, or constraints exist. `rtl/`, `tb/`, and `constraints/`
  are a target layout, not directories on disk.
- No simulator, synthesis flow, or programming utility has been selected.
- The hardware target is the Sipeed Tang Nano 9K
  ([`docs/boards/tang-nano-9k.md`](docs/boards/tang-nano-9k.md)).
- `docs/design/` holds no active plan; all plans are shipped and archived.

Do not create the target directories, RTL, or testbenches before a plan selects
a toolchain that can validate them. Work that cannot be simulated or built is
not implementable work.

## Global Rules

- Never invent requirements; ask when they are ambiguous.
- Never modify unrelated files.
- Prefer incremental changes; keep each commit focused on one task.
- Preserve existing project style.
- Explain important design decisions.
- Treat documentation as part of the implementation and update it with the
  change.
- Never claim behavior that is not implemented or verified.

Engineering philosophy is defined per role; see
[`.ai/roles/architect.md`](.ai/roles/architect.md).

## Source of Truth

When instructions conflict, use this priority:

1. User instructions
2. The active plan for the current task in `docs/design/`
3. [`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md) and
   [`docs/DECISIONS.md`](docs/DECISIONS.md)
4. Repository conventions
5. This file

If documentation and implementation disagree, report the inconsistency rather
than silently choosing one.

## Repository Layout

[`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md) is the single source of truth
for layout. It defines the responsibility of each top-level directory and the
board-aware structure to grow into once implementation begins.

Read it rather than copying it here — an earlier duplicate of that tree in this
file drifted out of sync twice. Note that most of those directories do not yet
exist; see [Current State](#current-state).

## Development Workflow

1. Understand the task.
2. Read or create the active plan.
3. Implement only the scope recorded in the plan.
4. Run the validation commands below and record the evidence in the plan.
5. Review the implementation against the plan's acceptance criteria.
6. Summarize changes and update the plan lifecycle status.
7. Stop.

### Validation

| Command | When |
| --- | --- |
| [`tools/check-doc-links`](tools/check-doc-links) | After any Markdown change, from the repository root. |
| `git diff --check` | Before any commit. |

These are the only validation tools that exist. Simulation, synthesis, and
timing validation are unavailable until a toolchain is selected; do not claim
any of them.

### Task Plans

Every task that changes architecture, RTL, verification, tooling, or
documentation needs an active plan. The plan is the working source of truth for
that task's scope, decisions, validation, and next steps.

- Create as `docs/design/YYYY-MM-DD-<slug>.md` from
  [`docs/PLAN_TEMPLATE.md`](docs/PLAN_TEMPLATE.md).
- Archive when shipped or paused as
  `docs/design/archive/YYYY-MM-DD-<slug>.md`, then repair relative links and
  run `tools/check-doc-links`.
- Record durable cross-task decisions in
  [`docs/DECISIONS.md`](docs/DECISIONS.md); plan-local decisions stay in the
  plan.

The Architect owns plan creation and readiness. Implementation roles read the
plan before changing files and record deviations and validation evidence in it.

Documentation-only corrections that change no requirement or architecture may
be made directly.

## Roles

Read the role charter before acting in a role; the table is an index, not the
charter. Use the smallest set of roles the task needs.

| Task | Role | Owns |
| --- | --- | --- |
| Requirements, architecture, decomposition, plans | [architect](.ai/roles/architect.md) | `docs/ARCHITECTURE.md`, `docs/DECISIONS.md`, `docs/design/`, and repository conventions and tooling — `AGENTS.md`, `.ai/roles/`, `tools/`, `.gitignore`, `.gitmessage` |
| Synthesizable HDL | [engineer](.ai/roles/engineer.md) | `rtl/` |
| Testbenches and behavioral validation | [verification-engineer](.ai/roles/verification-engineer.md) | `tb/` |
| Independent review of a change | [reviewer](.ai/roles/reviewer.md) | nothing — read-only |
| README, docs, plan archival, learning records | [documentation-guide](.ai/roles/documentation-guide.md) | `README.md`, `docs/` except `docs/ARCHITECTURE.md` and `docs/DECISIONS.md`; performs plan lifecycle mechanics in `docs/design/` |
| Board integration, constraints, build flow | deferred | — |

One role owns a file for a given task; concurrent roles must not edit the same
file.

An FPGA Integration role remains deferred until a toolchain is selected. The
board itself is already chosen, so board-specific work is blocked on tooling,
not on target selection.

## Delegation and Context Isolation

Roles do not by themselves create isolated execution contexts, so delegation
requires explicit triage. Before delegating, identify the task category,
primary and supporting roles, allowed files, non-goals, acceptance criteria,
required validation, and known risks.

Pass delegated work a bounded handoff packet:

```text
Task:
Active plan:
Role:
Allowed files:
Non-goals:
Acceptance criteria:
Required validation:
```

Delegated work must not rely on unrelated conversation history or expand scope.
Each delegated role reports changed files, validation evidence, assumptions,
open issues, and deviations from the plan. If independent delegation is
unavailable, perform the roles sequentially using the same boundaries.

The Reviewer evaluates the actual working tree and is read-only. The primary
agent remains responsible for final integration, acceptance-criteria
verification, and confirming that no unrelated changes were included.

## Git Commit Convention

```text
<type>(<scope>): <imperative summary>

<body>

<footer>
```

Supported types:

- `feat` — new functionality
- `fix` — defect correction
- `rtl` — synthesizable HDL change
- `test` — verification changes
- `docs` — documentation or plan changes
- `refactor` — structure-preserving code change
- `build` — toolchain or build changes
- `ci` — automation changes
- `chore` — maintenance
- `revert` — reversal of an earlier commit

Scope is repository-oriented — `rtl`, `tb`, `docs`, `tooling`, `ci`, or a
specific module.

Keep the subject concise and explain motivation or important design decisions
in the body.

```text
feat(rtl): add parameterized counter
test(counter): verify rollover behavior
docs(architecture): define clock and reset policy
fix(tb): correct reset sequencing
```

[`.gitmessage`](.gitmessage) carries the same format for interactive commits
(`git config commit.template .gitmessage`). Git strips it from the buffer, so
the types above are repeated here for agents using `git commit -m`. Hooks and
automated enforcement are deferred until the project needs them.

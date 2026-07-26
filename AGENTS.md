# AGENTS.md

# AI Agent Guide

Welcome to the FPGA Playground repository.

This file provides repository-wide instructions that apply to every AI agent working on this project.

Role-specific behavior is defined under `.ai/roles/`.

---

# Project Overview

This repository is an educational FPGA project.

The primary goal is to learn AI-assisted engineering while developing FPGA designs.

The project values maintainability, documentation, and engineering practices over implementation speed.

---

# Repository Layout

```
rtl/        Synthesizable HDL
tb/         Testbenches
docs/       Project documentation
tools/      Helper scripts
.ai/        AI roles, workflows and templates
```

---

# Global Rules

These rules apply to every AI role.

- Never invent requirements.
- Never modify unrelated files.
- Prefer incremental changes.
- Ask for clarification if requirements are ambiguous.
- Preserve existing project style.
- Explain important design decisions.
- Keep commits focused on a single task.

---

# Source of Truth

When making decisions, use the following priority:

1. User instructions
2. Current implementation task
3. Architecture documents in `docs/`
4. Repository conventions
5. This file

If documentation and implementation disagree, report the inconsistency rather than silently choosing one.

---

# Development Workflow

The standard workflow is:

1. Understand the task.
2. Read relevant documentation and create or update a plan based on
   [`docs/PLAN_TEMPLATE.md`](docs/PLAN_TEMPLATE.md).
3. Implement only the scope recorded in the plan.
4. Run project validation tools when available and record the evidence in the
   plan.
5. Review the implementation against the plan and acceptance criteria.
6. Summarize changes and update the plan lifecycle status.
7. Stop.

## Task Plans

Every new task that changes architecture, RTL, verification, tooling, or
documentation must have an active plan based on
[`docs/PLAN_TEMPLATE.md`](docs/PLAN_TEMPLATE.md). The plan is the working
source of truth for scope, non-goals, accepted decisions, validation, open
questions, and immediate next tasks.

Create active plans as `docs/design/YYYY-MM-DD-<slug>.md` and move shipped or
paused plans to `docs/design/archive/YYYY-MM-DD-<slug>.md`. Record durable,
cross-task decisions in [`docs/DECISIONS.md`](docs/DECISIONS.md); keep
plan-local decisions in the plan.

The Architect owns plan creation and readiness. Implementation roles must read
the plan before changing files and record relevant deviations or validation
evidence. The Reviewer uses the plan's review packet sections when a formal
review is requested. The Documentation Guide maintains plan links and archives
completed or paused plans according to the template instructions.

Small documentation-only corrections may be made directly when they do not
change requirements or architecture; otherwise, create a plan first.

---

# AI Roles

Role definitions are located in:

```
.ai/
└── roles/
    architect.md
    engineer.md
    verification-engineer.md
    reviewer.md
    documentation-guide.md
```

Choose the appropriate role for the current session.

The initial role set is:

- `architect` — requirements, architecture, decomposition, roadmap, and ADRs
- `engineer` — synthesizable RTL implementation under `rtl/`
- `verification-engineer` — testbenches and repeatable behavioral validation under `tb/`
- `reviewer` — independent review of implementation, verification, and documentation
- `documentation-guide` — project documentation, reproducibility, and learning records

Use the smallest set of roles needed for a task. The Architect prepares
implementation-ready work, the Engineer and Verification Engineer execute it,
and the Reviewer evaluates the result. The Documentation Guide records the
resulting decisions, workflow, and lessons learned.

An FPGA Integration role is intentionally deferred until a target board and
toolchain are selected. Until then, board-specific work must be treated as an
explicit architectural dependency rather than assumed.

Role files extend these global rules and may define additional responsibilities.

---

# Documentation

When making architectural changes, update documentation if necessary.

Documentation is considered part of the implementation.

---

# Git Commit Convention

Use the following format for new commits:

```text
<type>(<scope>): <imperative summary>

<body>

<footer>
```

Keep the subject concise and explain the motivation or important design
decisions in the body when needed. Use a repository-oriented scope such as
`rtl`, `tb`, `docs`, `tooling`, `ci`, or a specific module.

Supported types are:

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

Examples:

```text
feat(rtl): add parameterized counter
test(counter): verify rollover behavior
docs(architecture): define clock and reset policy
fix(tb): correct reset sequencing
```

Use the tracked [`.gitmessage`](.gitmessage) file as a local commit template
with `git config commit.template .gitmessage`. Commit hooks and automated
enforcement are deferred until the project needs them.

---

# Philosophy

Favor:

- Simple solutions
- Small commits
- Modular design
- Readability
- Testability

Avoid:

- Premature optimization
- Overengineering
- Large unrelated refactors
- Guessing user intent

When uncertain, ask.

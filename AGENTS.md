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
2. Read relevant documentation.
3. Implement only the requested scope.
4. Run project validation tools when available.
5. Summarize changes.
6. Stop.

---

# AI Roles

Role definitions are located in:

```
.ai/
└── roles/
    architect.md
    engineer.md
    reviewer.md
```

Choose the appropriate role for the current session.

Role files extend these global rules and may define additional responsibilities.

---

# Documentation

When making architectural changes, update documentation if necessary.

Documentation is considered part of the implementation.

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

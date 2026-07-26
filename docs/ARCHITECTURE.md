# FPGA Playground Architecture

## Purpose

FPGA Playground is an educational project for learning FPGA design and
AI-assisted engineering through small, maintainable, and testable examples.

The project targets a real development board so that simulation, synthesis, and
hardware behavior can eventually be connected. The initial hardware target is
the Sipeed Tang Nano 9K.

## Repository Boundaries

The intended responsibilities of the main directories are:

```text
rtl/          Synthesizable HDL
tb/           Simulation-only testbenches and verification support
constraints/  Board pin, timing, and implementation constraints
tools/        Repeatable development and validation commands
docs/         Architecture, decisions, plans, and learning records
```

As board-aware work begins, the expected organization is:

```text
rtl/
  core/                       Board-independent reusable RTL
  board/
    tang_nano_9k/             Tang Nano 9K wrappers and top-levels

tb/
  core/                       Core module testbenches
  board/                      Optional integration-level testbenches

constraints/
  tang_nano_9k/               Tang Nano 9K constraint files

tools/
  tang_nano_9k/               Board-specific build and programming helpers
```

This structure is a target organization, not a requirement to create empty
implementation files before a feature needs them.

## Hardware Target

The Tang Nano 9K is the primary and initially only supported hardware target.
Board-specific integration must be kept separate from reusable RTL so that
core modules can be simulated independently and potentially reused later.

Board facts and board-specific assumptions are maintained in
[`boards/tang-nano-9k.md`](boards/tang-nano-9k.md).

## RTL Boundary

Core RTL should not depend directly on board pins, board-specific clock names,
or vendor primitives unless the dependency is explicitly part of a documented
integration boundary.

Board integration is responsible for:

- connecting the board clock to the design
- defining reset behavior at the board boundary
- mapping logical signals to physical pins
- instantiating vendor-specific resources when necessary
- exposing a stable top-level suitable for implementation

## Clock and Reset Policy

The initial architecture favors single-clock designs. Each design must document
its input clock assumptions and any generated clocks.

Reset polarity, synchronization, and release behavior must be explicit at the
board boundary. Multi-clock designs and clock-domain crossings require a
separate documented decision.

## HDL and Naming Conventions

The project will use synthesizable HDL for RTL and keep simulation-only code in
`tb/`. The exact language version and tool support remain open decisions.

Initial conventions are:

- module names match their source filenames
- file and signal names use lowercase `snake_case`
- parameters use uppercase names
- magic numbers are replaced with named parameters or constants
- comments explain design intent and assumptions
- vendor-specific code is isolated and labeled

More detailed conventions should be added only when the first implementation
needs them.

## Verification Expectations

Every non-trivial core module should have a repeatable simulation testbench.
Verification should cover reset, normal operation, boundary behavior, and
module-specific error or rollover cases.

Hardware validation is complementary to simulation. A successful board demo
does not replace behavioral verification.

## Toolchain Policy

The project has not yet selected a simulator, synthesis flow, or programming
utility. The first hardware workflow should document exact tool versions and
provide one repeatable validation path.

The official Gowin flow is the initial reference for Tang Nano 9K hardware
implementation. Open-source tools may be evaluated later as a separate,
explicit tooling decision.

## Documentation and Decisions

- Cross-task architecture decisions belong in [`DECISIONS.md`](DECISIONS.md).
- Feature-specific scope and decisions belong in an active plan under
  `docs/design/`.
- Shipped or paused plans move to `docs/design/archive/`.
- Board facts belong in `docs/boards/`.
- Documentation must not imply that deferred implementation work is complete.

## Current Non-goals

The foundation does not yet define:

- a specific RTL feature or application
- a simulator or complete build flow
- pin constraint files
- synthesis settings
- a target clock frequency beyond the board input clock fact
- support for other FPGA boards
- a CPU, bus, display, or peripheral architecture

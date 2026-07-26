# Architecture Decisions

This file records durable decisions that apply across multiple tasks or plans.
Plan-local decisions belong in the relevant plan under `docs/design/`.

## Decision Format

For each durable decision, record:

- Date: `YYYY-MM-DD`
- Status: Proposed | Accepted | Superseded
- Decision: the concise decision statement
- Context: the problem or constraints
- Alternatives: the options considered
- Consequences: the resulting benefits, costs, and risks
- Related plans: links to affected task plans

## Decisions

- Date: `2026-07-26`
  Status: Accepted
  Decision: The Sipeed Tang Nano 9K is the project’s primary and initially only
  supported hardware target.
  Context: A concrete board gives the educational project a defined FPGA
  device, clock, I/O surface, and eventual hardware validation path.
  Alternatives: Remain board-agnostic; support multiple boards immediately.
  Consequences: Documentation and future integration will be board-aware, but
  reusable RTL must remain separate from board-specific wrappers. Supporting a
  second board will require an explicit architectural decision.
  Related plans: [`2026-07-26-tang-nano-9k-foundation.md`](design/archive/2026-07-26-tang-nano-9k-foundation.md)

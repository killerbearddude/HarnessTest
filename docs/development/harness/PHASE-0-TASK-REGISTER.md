# Phase 0 Task Register

## Authority and Scope

This register is the authoritative task-control record for **Phase 0 — Establish the Control Boundary**. It records only the tasks authorized for Phase 0 and does not authorize work outside Phase 0.

The harness may act only on the explicitly authorized current task. A task listed as later is not selected, planned, or started by this register.

## Phase 0 Status

- **Phase:** Phase 0 — Establish the Control Boundary
- **Phase status:** Active
- **Current task:** P0-T02 — Define the Phase 0 Task Register

## Phase 0 Task Register

| Sequence | Task ID | Title | Status |
| --- | --- | --- | --- |
| 1 | P0-T01 | Define Harness Autonomy Boundaries | Merged |
| 2 | P0-T02 | Define the Phase 0 Task Register | Current task |
| 3 | P0-T03 | Phase 0 task | Later Phase 0 task; not authorized to start |
| 4 | P0-GATE-01 | Phase 0 gate | Later Phase 0 task; not authorized to start |

## Dependency Sequence

```text
P0-T01 → P0-T02 → P0-T03 → P0-GATE-01
```

A successor task may not be selected or started solely because its predecessor is merged, reviewed, or otherwise complete. A new explicit `Proceed with next task.` instruction and task-specific authorization are required before any later task may be considered.

## Phase 1 Lock

**Phase 1 is locked.** No Phase 1 tasks are authorized, defined, selected, planned, or started by this register.

## Control Boundary

This register does not authorize:

- game code or game implementation work;
- GitHub workflows, CI configuration, or harness scripts;
- future-phase task definitions;
- project architecture or game-design documents; or
- selection or start of P0-T03, P0-GATE-01, or any Phase 1 work.

## Stop Condition

After one reviewable pull request for P0-T02 is opened, the harness must stop. No further task is selected or started.
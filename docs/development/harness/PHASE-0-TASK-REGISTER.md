# Phase 0 Task Register

## Authority and Scope

This is the authoritative task-control register for **Phase 0 — Establish the Control Boundary**. It defines only the approved Phase 0 sequence.

## Status Source

- **Phase:** Phase 0 — Establish the Control Boundary
- **Phase status:** Active
- **Status source:** GitHub pull-request evidence on the default branch

The harness derives task status during each repository check. This register has no manually maintained static current-task field.

## Approved Phase 0 Sequence

| Sequence | Task ID | Title | Evidence at this verification |
| --- | --- | --- | --- |
| 1 | P0-T01 | Define Harness Autonomy Boundaries | Completed: merged PR #2 |
| 2 | P0-T02 | Define the Phase 0 Task Register | Completed: merged PR #3 |
| 3 | P0-T03 | Repair Phase 0 task-register transition semantics | **Next eligible task**: no merged or open P0-T03 PR |
| 4 | P0-GATE-01 | Phase 0 gate | Later Phase 0 gate task |

```text
P0-T01 → P0-T02 → P0-T03 → P0-GATE-01
```

## Eligibility and Authorization

On `Proceed with next task.`, the harness checks GitHub and selects only the first approved Phase 0 task after completed tasks that has neither a merged PR nor an open PR.

- A merged PR marks its task completed.
- An open PR means its task is in review and is not eligible for another execution.
- The command authorizes execution of the one next eligible task already approved in this register.
- No separate task-specific authorization is required for an approved Phase 0 task.
- Eligibility is recalculated from GitHub evidence. A prior merge does not require a manual register update.

## One-Task-at-a-Time Rule

The harness executes one eligible task only. It does not select, plan, begin, or pre-stage a successor while a task has an open PR. After opening one PR, it stops. Review, approval, and merging remain outside the harness's authority.

## Phase 1 Lock

**Phase 1 is locked.** No Phase 1 tasks are authorized, defined, selected, planned, or started.

## Control Boundary

This register does not authorize game code, GitHub workflows, CI configuration, harness scripts, future-phase task definitions, project architecture documents, game-design documents, or Phase 1 work.

P0-GATE-01 remains a later Phase 0 gate task and is not selected or started while P0-T03 is eligible or open.

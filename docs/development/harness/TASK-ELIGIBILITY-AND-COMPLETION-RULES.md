# Task Eligibility and Completion Rules

## Purpose and Scope

This document defines deterministic rules for deriving task, gate-attempt, and phase state and selecting exactly one eligible harness task from repository-native authority. It is control policy only; it does not configure GitHub, CI, workflows, scripts, or implementation work.

## Evidence Sources and Precedence

State is derived in this order:

1. Current GitHub pull-request evidence determines review state, task completion, and gate-attempt completion.
2. The active phase register determines approved sequence, corrective path, qualifying closure gate, and phase state.
3. A merged gate report determines whether closure criteria are Pass, Fail, or Blocked and whether it recommends closure.
4. The executable definition determines a task's bounded authority.
5. The executable-definition format determines completeness.

Current GitHub PR evidence controls over stale static status wording. Merged evidence alone cannot override the qualifying-gate-result rule for phase closure.

## Distinct Completion and Closure States

Task completion, gate-attempt completion, and phase closure are distinct.

| State | Entry condition | Effect |
| --- | --- | --- |
| Completed task | Valid PR for the exact task merges into the default branch. | The task is not selected again normally. |
| Completed gate attempt | Valid phase-gate PR merges. | Evidence of a completed review attempt only. |
| Qualifying closure gate | The register designates the gate; its PR merges; its report records every required closure criterion as Pass; and its report explicitly recommends closure. | Closes only the named phase. |
| Non-qualifying gate attempt | A merged gate has any Fail or Blocked criterion, lacks a closure recommendation, or is not register-designated. | Does not close the phase or unlock a later phase. |

Each task has one lifecycle state: `blocked`, `ready`, `active`, `awaiting-review`, or `completed`. `phase-gate-pending` is supplementary phase control.

## Task Lifecycle States

| State | Entry condition | Exit condition | Selection effect |
| --- | --- | --- | --- |
| `completed` | Valid PR for task merges. | None normally. | Never selected again. |
| `awaiting-review` | Valid open task PR. | PR merges or closes without merge. | Blocks selection. |
| `active` | This invocation selected the sole ready task and work started without a PR. | PR opens, merge evidence appears, or later recomputation. | Blocks selection. |
| `ready` | All readiness conditions hold. | Selected, completed, given open PR, or condition changes. | Eligible for one explicit selection. |
| `blocked` | Required condition is absent, invalid, ambiguous, or conflicting. | Condition resolves and state is recomputed. | Must not be selected or executed. |

## Readiness and Blocking

A task is ready only when it is in the approved active-phase sequence or corrective path; its definition is complete and matches the register; predecessor and recorded repair conditions are merged; it is not completed, active, or awaiting-review; no other harness task is active or awaiting-review; no identity-conflict PR is open; the phase is active under these rules; and, for a qualifying gate, all register-required completion evidence exists.

Missing, invalid, ambiguous, or conflicting authority blocks a task. The harness must state the specific condition and must not infer omitted scope, successor work, validation, or later-phase authority.

## Gate Attempts and Phase Closure

A merged phase-gate PR is a completed gate attempt, not automatically a phase-closure event.

A phase closes only when all of the following are true:

1. The designated qualifying gate attempt is merged.
2. Its gate report records every required closure criterion as Pass.
3. Its report explicitly recommends phase closure.
4. The active phase register identifies that attempt as the qualifying closure gate.

A merged gate PR with any Blocked or Fail criterion does not close the phase, does not unlock a next phase, and remains valid evidence of a completed review attempt. Explicitly authorized corrective work is required before another gate attempt may occur.

A phase with a merged non-qualifying gate attempt remains active only when its register identifies an approved corrective path and a future qualifying gate task. Without both, phase state is blocked and no task may be selected.

`phase-gate-pending` exists only when the register identifies a qualifying gate, all required preceding work is complete, and that qualifying gate has not completed. A merged non-qualifying gate attempt does not satisfy or exit this state.

## Completion, Dependency, and Definition Rules

GitHub merged pull-request evidence is the sole completion authority for an exact task. A predecessor is satisfied only by valid merged evidence for that predecessor.

A task definition is complete only when it contains: task ID, phase, title, task type, predecessor dependency, task-state authority, purpose, exact allowed paths, forbidden scope, required authority documents, deliverable, acceptance criteria, validation, stop condition, and later-task boundary. A missing or invalid required field blocks execution.

## Active-Phase Derivation and Selection

A phase is active when its register authorizes execution and it has not closed through a qualifying closure gate. A later phase is not activated by any gate attempt, phase closure, empty queue, or absence of an earlier phase without explicit register authority.

On an explicit `Proceed with next task.` instruction, refresh PR evidence and authority documents, derive phase and task state, stop for any open task PR or authority conflict, select the one lowest approved ready item, perform only its approved scope, open at most one PR, and stop.

## Open Pull-Request Lock

Any open valid harness task PR, or an open PR with missing or conflicting identity, creates a repository-wide selection lock.

## Scope Boundary

These rules do not configure GitHub, CI, workflows, scripts, or automated enforcement. They do not create Phase 3 authority or select, define, plan, or start Phase 3 work.

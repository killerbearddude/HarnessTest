# Task Eligibility and Completion Rules

## Purpose and Scope

This document defines deterministic derivation of task, gate-attempt, phase, and system-planning-transition state. It selects exactly one ordinary executable task or, only when no ordinary task is ready, the bounded `SYS-PLAN-NEXT-TRANCHE` transition. It is control policy only and does not configure GitHub, CI, workflows, scripts, or implementation work.

## Evidence Sources and Precedence

State is derived in this order:

1. Current GitHub pull-request evidence determines review state, task completion, and gate-attempt completion.
2. Active and closed phase registers determine approved task sequence, corrective path, qualifying closure gates, and phase state.
3. Merged gate reports determine whether closure criteria are Pass, Fail, or Blocked and whether closure is recommended.
4. `PHASE-ROADMAP.md` determines whether exactly one future phase is ready for bounded planning.
5. `SYSTEM-PLANNING-RULES.md` determines the eligibility and permitted output of `SYS-PLAN-NEXT-TRANCHE`.
6. Executable task definitions determine task-level bounded authority.
7. `EXECUTABLE-TASK-DEFINITION-FORMAT.md` determines definition completeness.

Current GitHub PR evidence controls over stale static status wording. Merged evidence alone cannot override qualifying-gate rules for phase closure or system-planning trigger conditions.

## Distinct States

Task completion, gate-attempt completion, phase closure, and system-planning eligibility are distinct states.

| State | Entry condition | Effect |
| --- | --- | --- |
| Completed task | Valid PR for the exact task merges into the default branch. | The task is not selected again normally. |
| Completed gate attempt | Valid phase-gate PR merges. | Evidence of a completed review attempt only. |
| Qualifying closure gate | The register designates the gate; its PR merges; its report records every required closure criterion as Pass; and its report explicitly recommends closure. | Closes only the named phase. |
| Non-qualifying gate attempt | A merged gate has any Fail or Blocked criterion, lacks a closure recommendation, or is not register-designated. | Does not close the phase or unlock a later phase. |
| `SYS-PLAN-NEXT-TRANCHE` eligible | No normal ready task exists and every system-planning trigger condition passes. | Authorizes one bounded planning PR only. |

Each ordinary task has one lifecycle state: `blocked`, `ready`, `active`, `awaiting-review`, or `completed`. `phase-gate-pending` is supplementary phase control.

## Ordinary Task Readiness and Blocking

An ordinary task is ready only when it is in the approved active-phase sequence or corrective path; its definition is complete and matches the register; predecessor and recorded repair conditions are merged; it is not completed, active, or awaiting-review; no other harness task is active or awaiting-review; no identity-conflict PR is open; the phase is active; and, for a qualifying gate, all register-required completion evidence exists.

Missing, invalid, ambiguous, or conflicting authority blocks a task. The harness must state the specific condition and must not infer omitted scope, successor work, validation, or later-phase authority.

## Gate Attempts and Phase Closure

A merged phase-gate PR is a completed gate attempt, not automatically a phase-closure event.

A phase closes only when all of the following are true:

1. The designated qualifying gate attempt is merged.
2. Its gate report records every required closure criterion as Pass.
3. Its report explicitly recommends phase closure.
4. The active phase register identifies that attempt as the qualifying closure gate.

A merged gate PR with any Blocked or Fail criterion does not close the phase, does not unlock a later phase, and remains valid evidence of a completed review attempt. Explicitly authorized corrective work is required before another gate attempt may occur.

A phase with a merged non-qualifying gate attempt remains active only when its register identifies an approved corrective path and a future qualifying gate task. Without both, phase state is blocked and no task or planning transition may be selected.

## Completion, Dependency, and Definition Rules

GitHub merged pull-request evidence is the sole completion authority for an exact task. A predecessor is satisfied only by valid merged evidence for that predecessor.

A task definition is complete only when it contains task ID, phase, title, task type, predecessor dependency, Task-state authority, purpose, exact allowed paths, forbidden scope, required authority documents, deliverable, acceptance criteria, validation, stop condition, and later-task boundary. A missing or invalid required field blocks execution.

## System Planning Transition

`SYS-PLAN-NEXT-TRANCHE` is not an ordinary phase task. Its trigger conditions, selection boundary, permitted output, format-validation requirement, prohibited actions, post-merge behavior, and controlled-stop behavior are defined by `SYSTEM-PLANNING-RULES.md`.

The transition is eligible only when every trigger condition in that document passes, including no valid open harness PR, no active or awaiting-review task, no active phase with a ready executable task, qualifying closure of the most recent active phase or no active phase, exactly one `ready_for_planning` roadmap entry, complete roadmap fields, existing and specific source authority, and no unresolved authority conflict.

The transition cannot activate a later phase, execute implementation, or select a generated future task. It may create only the single bounded planning PR permitted by `SYSTEM-PLANNING-RULES.md`.

## Active-Phase Derivation and Selection

A phase is active when its merged register authorizes execution and it has not closed through a qualifying closure gate. A later phase is not activated by a gate attempt, phase closure, empty queue, or absence of an earlier phase without a merged register created under approved planning authority.

On an explicit `Proceed with next task.` instruction, the harness must:

1. Refresh protected-default-branch state, current GitHub PR evidence, applicable phase registers, task definitions, roadmap, and required authority documents.
2. Stop if any valid harness PR is open, any task is active or awaiting review, or authority conflict prevents reliable derivation.
3. Derive ordinary ready tasks in the active phase.
4. Select exactly one ordinary task when the ready set is non-empty: the lowest approved sequence item.
5. Only when the ordinary ready set is empty, evaluate `SYS-PLAN-NEXT-TRANCHE` under `SYSTEM-PLANNING-RULES.md`.
6. Select the transition only if every trigger condition is true and it is the sole eligible system planning transition.
7. Otherwise enter a controlled stop and report the smallest missing roadmap, product, architecture, contract, source-authority, or Project Owner decision.
8. Perform only the selected ordinary task or system transition, open at most one PR, and stop.

A `Proceed with next task.` instruction does not authorize concurrent work, an out-of-sequence task, automatic implementation, scope missing from approved authority, or planning for a roadmap phase that is not eligible.

## Open Pull-Request Lock

Any open valid harness task or planning PR, or an open PR with missing or conflicting identity, creates a repository-wide selection lock.

## Scope Boundary

These rules do not configure GitHub, CI, workflows, scripts, or automated enforcement. They do not create Phase 3 authority beyond the approved roadmap planning boundary and do not select, define, plan, or start a Phase 3 tranche except through a later eligible `SYS-PLAN-NEXT-TRANCHE` selection.
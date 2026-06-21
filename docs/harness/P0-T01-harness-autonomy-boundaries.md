# P0-T01 — Harness Autonomy Boundaries

## Status

- **Phase:** Phase 0 — Establish the Control Boundary
- **Task:** P0-T01 — Define Harness Autonomy Boundaries
- **Applies to:** Harness-control work only

## Purpose

This policy defines the limits of harness initiative. It prevents workflow progression, scope expansion, and pull-request finalization from occurring by inference rather than by explicit user authorization.

## Authoritative State

Before beginning an authorized task, the harness must inspect the repository state needed to establish the control boundary. At minimum, this includes:

1. The protected/default branch and its current state.
2. Open pull requests that could overlap the active task.
3. Merged or closed pull requests relevant to the active task.
4. Existing repository material that governs the active task.

Repository state is authoritative over chat memory for branch, pull-request, and completion status.

## Authorization Boundary

The harness may begin work only when all of the following are true:

1. An active phase and active task are explicitly identified.
2. The user explicitly authorizes progression by saying **`Proceed with next task.`**
3. Repository inspection does not show that the task is already represented by an unresolved or completed reviewable result.
4. The proposed work remains within the active task's approved scope.

The authorization applies only to the identified active task. It does not authorize selection, planning, or execution of any later task.

## Permitted Harness Actions

For the explicitly authorized active task, the harness may:

- Inspect the repository state necessary to verify task eligibility and avoid overlap.
- Create a bounded, reviewable change that implements only the active task.
- Open one pull request for that change and report its review status.
- Identify missing or conflicting authority that blocks a safe decision.

A task may use a branch and pull request as its review boundary, but the harness must not treat creation of that pull request as authorization for anything beyond the task itself.

## Prohibited Harness Actions

The harness must not:

- Select, draft, plan, begin, or pre-stage a later task without a new explicit user authorization.
- Advance, close, or otherwise change a phase based on task completion, pull-request creation, review activity, or a merge.
- Infer authorization from a merged pull request, an empty queue, elapsed time, or conversational context.
- Merge, approve, enable auto-merge for, or otherwise finalize a pull request.
- Modify product, game, architecture, contract, evaluator, balance, or UX work when the active phase restricts work to harness controls.
- Expand the active task to resolve unrelated issues discovered during repository inspection.

## Ambiguity and Missing Authority

When the active task lacks sufficient approved authority, the harness must not guess. It must stop at the boundary, state the missing decision or contract, and limit any recommendation to the smallest bounded item needed to unblock the current work. It must not create, select, or start that item without explicit authorization.

## Pull-Request Review Boundary

A pull request is a reviewable result, not evidence of final acceptance. The harness may open the pull request and summarize its scope, but it must stop after doing so. User review and any merge decision remain outside the harness's authority.

A merge proves only that the represented task has completed in the repository. It does not authorize phase advancement or the next task.

## Explicit Stop Condition

After opening one pull request for the active task, the harness must stop. Its final status must state that:

1. The active task has produced one reviewable result.
2. No further task was selected or started.
3. A new explicit **`Proceed with next task.`** instruction is required before any subsequent task may be considered.

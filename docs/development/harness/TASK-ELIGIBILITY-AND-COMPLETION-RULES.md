# Task Eligibility and Completion Rules

## Purpose and Scope

This document defines deterministic rules for deriving harness task state and selecting exactly one eligible task from repository-native authority. It is a control-policy document only. It does not configure GitHub, branch protections, CI, workflows, scripts, or implementation work.

## Evidence Sources and Precedence

Task state is derived from current repository evidence in the following order:

1. Current GitHub pull-request evidence determines review state and completion.
2. The active phase register determines the approved sequence, phase-gate identity, and any recorded one-time eligibility constraints.
3. The executable task definition determines the task's scope, deliverable, acceptance criteria, validation, and stop condition.
4. The executable-task-definition format determines whether a task definition is complete.

A valid task pull request identifies exactly one approved task ID and phase and targets the repository default branch. A pull request with absent, conflicting, duplicated, or unapproved task identity creates an authority conflict.

Current GitHub pull-request evidence controls over static task-status wording in registers, definitions, reports, branches, commits, or checklists. Static prose cannot complete a task, satisfy a dependency, or override an open pull request.

## Derived Task States

Each task has one lifecycle state: `blocked`, `ready`, `active`, `awaiting-review`, or `completed`. `phase-gate-pending` is a supplementary phase-control state; it does not replace the lifecycle state of the gate task.

| State | Objective entry condition | Exit condition | Selection effect |
| --- | --- | --- | --- |
| `completed` | A valid pull request for the task is merged into the default branch. | None during normal derivation. Corrective work requires separately approved authority. | Never selected again. |
| `awaiting-review` | The task is not completed and has a valid open task pull request. | The PR merges, or closes without merge and state is recomputed. | Blocks all new harness-task selection. |
| `active` | This invocation selected the task as the sole ready task and work has started, but no task PR has been opened and no merged evidence exists. | A PR opens, merged evidence appears, or execution ends and state is recomputed later. | Blocks all other harness-task selection. |
| `ready` | Every readiness condition in this document is true. | The task is selected, completed, receives an open task PR, or a readiness condition becomes false. | Eligible for one explicit selection command. |
| `blocked` | The task is not completed, awaiting-review, active, or ready because at least one required condition is absent, invalid, or conflicting. | The blocking condition is resolved and state is recomputed. | Must not be selected, planned, pre-staged, or executed. |

### Completed

Completion is established only by valid GitHub merged-pull-request evidence for the exact task. Closed-but-unmerged pull requests, approvals, CI outcomes, reviews, branch commits, and status prose are not completion evidence.

### Awaiting-review

Opening a valid task pull request changes the task to `awaiting-review`. The harness must stop after opening it and must not approve, merge, or claim completion before merged evidence exists. If the pull request closes without merge, the task is not completed; eligibility is recomputed from current authority and evidence.

### Active

`Active` exists only during the current harness execution after a valid `Proceed with next task.` instruction selected one ready task. It is not established by a branch or unmerged commit. A task cannot remain active across a later invocation without current execution evidence; it is recomputed as `ready` or `blocked` unless it has moved to `awaiting-review` or `completed`.

### Ready

A task is `ready` only when all of the following are true:

1. The task is in the approved sequence of the active phase.
2. Its executable task definition is present, complete, internally consistent, and matches the task ID and phase in the register.
3. Its direct predecessor has valid merged-pull-request completion evidence, or the definition explicitly states that it has no predecessor.
4. Any additional one-time repair or eligibility condition recorded in the active phase register has valid merged completion evidence.
5. The task is not `completed`, `active`, or `awaiting-review`.
6. No other harness task is `active` or `awaiting-review`.
7. No open pull request with missing or conflicting harness-task identity exists.
8. The phase is active and has not closed through merged phase-gate evidence.
9. For a phase gate, every task the gate requires as completion evidence is completed.

`Ready` means eligible for selection; it does not itself authorize work.

### Blocked

A task is `blocked` when any readiness requirement is unsatisfied or cannot be deterministically evaluated. Typical causes include an unmet predecessor, an incomplete or conflicting definition, a missing authority document, an inactive or ambiguous phase, an open task PR, an unresolved PR-identity conflict, or a required one-time repair that is not merged.

The harness must report the specific unsatisfied condition and must not infer missing paths, deliverables, acceptance criteria, validation, dependencies, or later-phase authority.

### Phase-gate-pending

A phase is `phase-gate-pending` when every non-gate task required by its approved sequence is completed, the gate definition is complete, and the gate has not yet completed. The gate task may then be `ready`, `active`, or `awaiting-review` under the normal lifecycle rules.

A phase does not close merely because it is phase-gate-pending or because its gate PR is open. It closes only when a valid gate pull request merges. A merged gate closes only that phase; it does not activate or authorize a later phase by implication.

## Completion, Dependency, and Definition Rules

GitHub merged-pull-request evidence is the sole completion authority. A predecessor dependency is satisfied only by valid merged evidence for the exact predecessor task.

A task definition is complete only when it contains the metadata and narrative sections required by `EXECUTABLE-TASK-DEFINITION-FORMAT.md`: task ID, phase, title, task type, predecessor dependency, task-state authority, purpose, exact allowed paths, forbidden scope, required authority documents, required deliverable, acceptance criteria, required validation, stop condition, and later-task boundary.

A missing, invalid, ambiguous, or conflicting required definition field blocks task execution. The task register alone does not supply omitted task-level authority.

## Active-Phase Derivation

A phase is active only when its approved register authorizes execution and no valid merged pull request exists for the phase gate that its register defines as closing the phase. The current repository must identify one unambiguous active phase for selection to proceed.

If zero phases, multiple phases, or conflicting phase-gate evidence appear active, task selection is blocked until approved repository authority resolves the conflict. A later phase is not activated by the closure, absence, or incomplete authority of an earlier phase.

## Selection Procedure

On an explicit `Proceed with next task.` instruction, the harness must:

1. Refresh current GitHub pull-request evidence and read the applicable phase register, executable task definitions, and required authority documents from the default branch.
2. Derive the active phase and each approved task's lifecycle state using these rules.
3. Stop without selecting work if any harness task is `active` or `awaiting-review`, or if an authority conflict prevents reliable derivation.
4. Build the set of `ready` tasks in the active phase.
5. Select exactly one task: the ready task with the lowest approved sequence number.
6. Treat a missing sequence, equal sequence numbers, or any other tie that prevents a unique selection as an authority conflict; select no task.
7. Mark only the selected task `active` for the current execution and perform only its approved scope.
8. Open at most one task PR, then stop. Do not select, plan, begin, or pre-stage a successor.

A `Proceed with next task.` instruction does not authorize concurrent work, an out-of-sequence task, a phase transition, or scope missing from the selected task's executable authority.

## Open Pull-Request Lock

Any open valid harness task pull request creates a repository-wide harness selection lock. While the lock exists, no other task is ready, no successor or concurrent task may be selected, and the harness must await human review and merge or closure of the open pull request.

An open pull request with missing or conflicting task identity also creates a selection lock. The harness must report the conflict rather than guess which task it represents.

## Scope Boundary

These rules define task-state derivation only. They do not configure or claim enforcement of GitHub settings, branch protections, human approval, CI, workflows, scripts, or automated validation. They do not select, define, plan, or start P2-T04, P2-GATE-01, or any Phase 3 work.

# Task Eligibility and Completion Rules

## Purpose

These rules derive generic harness task state from source-backed authority. They distinguish long-range catalog planning, executable-horizon permission, task completion, qualifying phase closure, and phase retirement.

## Evidence Order

1. Current GitHub PR evidence determines whether a task is awaiting review and whether an exact task identity has merged.
2. Current Project Owner decisions determine retirement, direct bounded tasks, source approval, and external-control attestation.
3. The active conversion or project register determines the executable horizon, sequence, and qualifying gate.
4. The source manifest, roadmap, and full task catalog determine source-backed planning authority.
5. The active executable task definition determines scope, deliverable, validation, and stop condition.

GitHub evidence controls over stale task-status prose. A catalog entry or a merged PR cannot override an active-register requirement.

## Task States

| State | Meaning |
| --- | --- |
| blocked | Required source authority, dependency, attestation, or definition is missing or conflicting. |
| ready | The task is in the active executable horizon and all eligibility conditions pass. |
| active | The task is selected and no PR is open. |
| awaiting-review | The exact task has one open valid PR. |
| completed | A valid PR for the exact task identity has merged. |
| retired | The Project Owner has retired the pilot or task sequence; it is preserved as history and cannot be selected. |

A retired task or phase is not completed merely because prior PRs merged. Retirement cannot satisfy a predecessor, qualifying gate, or later-phase entry condition.

## Exact Task Identity

Completion and dependency evidence require a merged PR whose canonical `**Task:**` identity equals the task ID exactly. Arbitrary title, body, deferred-work, or archive mentions do not satisfy identity evidence. A task with exact merged completion evidence cannot be selected again.

A generic task identity is uppercase and uses one of these forms:

```text
<PROGRAM>-PLAN-<NN>
<PROGRAM>-T<NN>
<PROGRAM>-GATE-<NN>
```

`<PROGRAM>` is an authority-defined uppercase program identifier. The identity does not imply a product, stack, or phase name.

## Executable Readiness

A task is ready only when all of the following are true:

1. it is listed in the active register's executable horizon;
2. its full task definition is complete, including Task-state authority before Purpose;
3. it has exact allowed paths, bounded deliverable, acceptance criteria, validation, stop condition, and later-task boundary;
4. all exact predecessor and decision dependencies are satisfied;
5. required source-authority documents remain approved in the source manifest;
6. required external-control attestations or independent evidence are current where applicable;
7. it has no exact merged completion evidence;
8. no valid harness PR is open; and
9. no other task is active or awaiting review.

The lowest ready task in the active register sequence is selected. A full task catalog item that is not in the executable horizon is never executable merely because it is planned.

## Phase Closure and Retirement

A phase closes only when its register-designated qualifying gate merges with a report that records every closure criterion as Pass and explicitly recommends closure.

A direct Project Owner retirement decision may retire a non-implementation pilot phase without a qualifying gate. The decision must preserve an archive or archive map, identify successor authority, state that retirement is not completion, and state whether any implementation phase remains active. Retired pilot work is excluded from all readiness, horizon, and successor derivation.

## Proceed Selection

On `Proceed with next task.`, the harness must:

1. refresh default-branch, PR, register, source-manifest, roadmap, catalog, horizon, and task-definition evidence;
2. stop if any valid harness PR is open or authority conflicts;
3. exclude retired pilot work;
4. derive ready tasks only from the active executable horizon;
5. select exactly one lowest ready task or report the smallest missing authority;
6. perform only that work unit, open at most one PR, and stop.

The generic template-conversion register becomes this repository's active authority only after its introducing PR merges. Until a new project supplies approved source documents and bootstrap artifacts, no project implementation phase is active.

## Scope Boundary

These rules do not configure GitHub settings, workflows, CI, scripts, or implementation. They do not create product-specific authority.
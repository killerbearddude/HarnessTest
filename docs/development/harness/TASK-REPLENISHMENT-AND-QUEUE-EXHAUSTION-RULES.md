# Task Replenishment and Queue Exhaustion Rules

## Purpose and Scope

This document defines how the harness maintains an approved executable-task horizon and how it stops when that horizon is depleted or incomplete. It governs task-control and planning boundaries only. It does not create a task, select work, authorize implementation, configure GitHub, configure CI, create workflows, or create scripts.

## Terms

### Approved Task Queue

The **approved task queue** is the ordered set of tasks in the active phase register that have repository-native executable authority. A queue entry is executable only when its task definition is complete, internally consistent, and satisfies the eligibility rules in `TASK-ELIGIBILITY-AND-COMPLETION-RULES.md`.

### Queue Horizon

The **queue horizon** is the number of approved executable tasks that remain after the task currently being executed or awaiting review. A task that is blocked, lacks complete executable authority, has an unmet dependency, or belongs to another phase does not count toward the horizon.

A phase gate is a closure task, not an implementation successor. A phase gate does not count toward the minimum approved-task horizon for an implementation phase.

### Active Implementation Phase

An **active implementation phase** is a phase explicitly authorized by the Project Owner to modify implementation work. A requirements, policy, task-authoring, or gate phase is not an implementation phase merely because it is active.

### Controlled Stop State

A **controlled stop state** exists when the active phase has no ready task with complete executable authority that may be selected under the eligibility rules. It is a phase-control state, not a substitute for a task lifecycle state.

## Minimum Approved-Task Horizon

An active implementation phase must maintain a minimum horizon of **one approved executable successor task** beyond the task currently being executed or awaiting review.

The successor must:

1. Be listed in the active phase register after the current task.
2. Have a complete executable task definition with exact paths, scope, deliverable, acceptance criteria, validation, stop condition, and later-task boundary.
3. Be capable of becoming ready when its predecessor completion evidence exists.
4. Not be blocked by missing, ambiguous, or conflicting authority.

The horizon is assessed before selecting an implementation task, after opening its pull request, and after its pull request merges or closes. A phase may temporarily fall below the horizon only by entering the controlled stop state described below; it must not compensate by inferring, drafting, or starting unapproved work.

## Queue Exhaustion and Absent Authority

The harness must enter the controlled stop state when any of the following applies:

- The active phase has no ready task with complete executable authority.
- The next task in sequence is missing an executable definition, a required field, a required authority document, or a deterministic dependency rule.
- The approved queue has no successor task beyond the current task in an active implementation phase.
- The remaining candidate is a phase gate but no authorized implementation successor exists to satisfy the required horizon.
- Repository evidence, phase identity, task sequence, task identity, or pull-request evidence is missing, ambiguous, or conflicting.

In a controlled stop state, the harness must:

1. Stop task selection and execution.
2. State the specific missing authority, dependency, or queue condition.
3. Preserve the distinction between repository evidence and static prose.
4. Avoid creating branches, commits, pull requests, task definitions, implementation changes, or phase transitions unless separately authorized.
5. Wait for explicit, bounded authority before any replenishment action.

A merged pull request, an empty queue, elapsed time, an earlier conversation, or the absence of objections does not authorize replenishment.

## Replenishment Assessment

The harness must assess queue horizon at these control points:

- before executing a selected task;
- after a task pull request is opened;
- after a task pull request is merged or closed without merge;
- before selecting a phase gate; and
- whenever the current active phase or task authority changes.

The assessment must use current GitHub pull-request evidence, the active phase register, executable task definitions, and applicable authority documents. Current GitHub evidence controls over stale task-status wording.

If one or more approved executable successors satisfy the horizon, the harness follows the ordinary one-task-at-a-time selection rules. It does not pre-stage a successor while a task is active or awaiting review.

## Bounded Planning and Task-Authoring Work

A planning or task-authoring pull request may be created only when all of the following conditions are satisfied:

1. The Project Owner explicitly authorizes a bounded planning, task-authoring, corrective, or phase-setup task; or an already-approved executable task definition explicitly authorizes that exact planning or task-authoring work.
2. The work has one task ID, one active phase, exact allowed paths, explicit forbidden scope, required authority documents, a bounded deliverable, acceptance criteria, validation, a stop condition, and a later-task boundary.
3. No harness task is active or awaiting human review, and no open harness task pull request creates a selection lock.
4. The work is limited to the authorized planning or task-authoring paths and does not resolve unrelated authority gaps by inference.
5. The resulting pull request states the missing authority or queue condition, the bounded outcome, validation evidence, deferred work, and that no implementation task was started.

Queue exhaustion alone does not authorize a planning or task-authoring pull request. It identifies the need for bounded authority; it does not supply that authority.

## Separation from Implementation Work

Planning, task-authoring, corrective, and phase-setup work are not implementation work.

Such work must not:

- modify game or product implementation;
- modify repository settings, branch protections, workflows, CI configuration, or scripts;
- claim that implementation enforcement is configured or active;
- create product, architecture, game-design, evaluator, content, diagnostics, persistence, or UI authority beyond its approved scope; or
- select, draft, pre-stage, or begin an implementation task.

Implementation work may begin only when the Project Owner has explicitly authorized the implementation phase and the selected implementation task has complete executable authority and is ready under the eligibility rules.

## Missing Direction or Domain Authority

The harness must enter the controlled stop state when any required authority is missing, ambiguous, or conflicting, including:

- project direction or business objective;
- product, game-design, architecture, contract, evaluator, content, diagnostics, persistence, or UI authority;
- active-phase authority;
- executable task authority;
- dependency or completion evidence; or
- required validation authority.

The harness must report the smallest bounded decision, contract, task-authoring item, or corrective item needed to resolve the specific gap. It must not invent product direction, architecture, contracts, implementation scope, validation, or successor tasks.

## New Phases, New Scope, and Implementation Authorization

A new phase, a new scope category, or implementation work requires explicit Project Owner authorization. A merged phase gate closes only the phase named by that gate; it does not activate a later phase, authorize task creation, or authorize implementation.

A task register, planning artifact, or replenishment assessment may describe only authority that has already been approved. It cannot create Phase 3 or later authority by implication.

## Pull-Request and Stop Boundary

A bounded planning or task-authoring task follows the same one-task-at-a-time and pull-request boundary as every harness task. The harness may open one reviewable pull request for that task and must then stop for human review. It may not approve, merge, enable auto-merge, or claim completion before valid merged GitHub pull-request evidence exists.

## Scope Boundary

These rules do not create Phase 3 tasks, implementation tasks, product or architecture authority, repository settings, branch protections, workflows, CI configuration, scripts, or automation. They do not select, define, plan, or start P2-GATE-01 or any Phase 3 work.

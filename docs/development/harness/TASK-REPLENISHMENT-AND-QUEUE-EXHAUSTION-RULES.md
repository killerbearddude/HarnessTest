# Task Replenishment and Queue Exhaustion Rules

## Purpose and Scope

This document defines how the harness maintains executable-task authority, handles a depleted queue, and invokes the bounded roadmap planner when normal task selection is exhausted. It governs task-control and planning boundaries only. It does not create implementation work, configure GitHub, configure CI, create workflows, or create scripts.

## Terms

### Approved Task Queue

The **approved task queue** is the ordered set of tasks in an active phase register that have repository-native executable authority. A queue entry is executable only when its task definition is complete, internally consistent, and eligible under `TASK-ELIGIBILITY-AND-COMPLETION-RULES.md`.

### Queue Horizon

The **queue horizon** is the number of approved executable tasks that remain after the task currently being executed or awaiting review when a phase is subject to a successor-horizon requirement. A task that is blocked, lacks complete authority, has an unmet dependency, or belongs to another phase does not count.

A phase gate is a closure task, not an implementation successor. It does not count toward the minimum approved-task horizon for an active implementation phase.

### Active Implementation Phase

An **active implementation phase** is a phase explicitly authorized by the Project Owner to modify implementation work. A requirements, policy, task-authoring, governance, documentation, control, planning, or gate phase is not an implementation phase merely because it is active.

### Controlled Stop State

A **controlled stop state** exists when no ordinary ready task or eligible system planning transition may be selected under current authority. It is a control state, not a substitute for a task lifecycle state.

A controlled stop caused solely by implementation-successor horizon or phase-gate successor-horizon requirements applies only to an active implementation phase.

## Minimum Approved-Task Horizon

An active implementation phase must maintain a minimum horizon of **one approved executable successor task** beyond the task currently being executed or awaiting review.

The successor must be in the active phase register after the current task, have a complete executable definition, be capable of becoming ready when predecessor evidence exists, and not be blocked by missing, ambiguous, or conflicting authority.

The horizon is assessed before selecting an implementation task, after opening its pull request, and after its pull request merges or closes. An active implementation phase may temporarily fall below the horizon only by entering the controlled stop state; it must not compensate by inferring, drafting, or starting unapproved implementation work.

## Queue Exhaustion and Roadmap Replenishment

The harness enters the controlled stop state when any of the following applies:

- An active phase has no ordinary ready task with complete executable authority and `SYS-PLAN-NEXT-TRANCHE` is not eligible.
- The next task in sequence is missing an executable definition, required field, required authority document, or deterministic dependency rule.
- The approved queue has no successor task beyond the current task in an active implementation phase and no separately approved replenishment authority applies.
- In an active implementation phase, the remaining candidate is a phase gate but no authorized implementation successor exists to satisfy the required horizon.
- Repository evidence, phase identity, task sequence, task identity, roadmap state, or pull-request evidence is missing, ambiguous, or conflicting.

A depleted or closed normal queue does not by itself authorize planning. When no ordinary task is ready, the harness must evaluate `SYS-PLAN-NEXT-TRANCHE` under `SYSTEM-PLANNING-RULES.md` and `PHASE-ROADMAP.md`.

The roadmap planner may be selected only when every system-planning trigger condition passes. If exactly one roadmap phase is `ready_for_planning` with complete, specific source authority, the next `Proceed with next task.` may select the planner. If no qualifying roadmap entry exists, multiple entries qualify, source authority is missing or insufficient, or any other trigger condition fails, the harness remains in controlled stop and reports the smallest missing authority or owner decision.

## Governance, Documentation, and Control Phase Completion

A governance, documentation, or control phase may validly end with its register-designated qualifying gate as its final approved item. Such a phase does not require a successor implementation task merely because its final item is a gate.

The absence of an implementation successor must not create a controlled stop for a governance, documentation, or control phase whose qualifying gate is ready under the eligibility and qualifying-gate lifecycle rules.

## Replenishment Assessment

The harness must assess normal queue horizon before executing an implementation task, after an implementation-task PR opens, after an implementation-task PR merges or closes, before selecting a phase gate in an active implementation phase, and when an active implementation phase or its authority changes.

It must assess roadmap planning eligibility whenever no ordinary ready task exists. The assessment uses current GitHub evidence, active and closed phase registers, executable definitions, `PHASE-ROADMAP.md`, `SYSTEM-PLANNING-RULES.md`, and applicable source authority. Current GitHub evidence controls over stale prose.

Normal ready-task selection has priority. The planner cannot pre-stage a successor while any task is active or awaiting review.

## Bounded Planning and Task-Authoring Work

A planning or task-authoring PR may be created only through one of these approved paths:

1. an explicit bounded Project Owner authorization;
2. an already-approved executable task definition that authorizes the exact work; or
3. an eligible `SYS-PLAN-NEXT-TRANCHE` selection under the roadmap and system-planning rules.

In all cases, no valid harness PR may be open, the work must remain within approved planning boundaries, it must not resolve unrelated gaps by inference, and its PR must state authority, bounded output, validation, deferred work, and that implementation was not started.

`SYS-PLAN-NEXT-TRANCHE` does not authorize an unbounded backlog or a second planning PR. It authorizes only the exact register, three-to-five executable definitions, and qualifying gate definition permitted by `SYSTEM-PLANNING-RULES.md`.

## Separation from Implementation Work

Planning, task-authoring, corrective, phase-setup, and system-planning work are not implementation work. They must not modify game or product implementation, GitHub settings, branch protections, workflows, CI configuration, scripts, or unapproved product, architecture, game-design, evaluator, content, diagnostics, persistence, or UI authority.

Implementation may begin only when the Project Owner has authorized the implementation phase, a merged phase register exists, and the selected implementation task has complete executable authority and is ready under eligibility rules.

## Missing Direction or Domain Authority

The harness must remain in controlled stop when required project direction, product, game-design, architecture, contract, evaluator, content, diagnostics, persistence, UI, active-phase authority, executable authority, dependency evidence, validation authority, roadmap authority, or source authority is missing, ambiguous, or conflicting.

It must report the smallest bounded decision, contract, task-authoring item, roadmap correction, or owner direction needed. It must not invent behavior, validation, scope, or successors.

## New Phases, New Scope, and Implementation Authorization

A roadmap entry may authorize only bounded planning through `SYS-PLAN-NEXT-TRANCHE`. It cannot activate a phase or authorize implementation before the resulting planning PR merges.

A merged qualifying gate closes only its named phase. A merged planning PR makes the planned phase active only under the register created by that PR. A later explicit `Proceed with next task.` is still required to select an executable task in the planned phase.

## Pull-Request and Stop Boundary

Every bounded planning or task-authoring action follows the one-task-at-a-time and one-PR boundary. The harness opens one reviewable PR and then stops for human review and squash merge. It may not approve, merge, enable auto-merge, or claim completion before valid merged GitHub evidence exists.

## Scope Boundary

These rules do not create Phase 3 tasks, implementation tasks, repository settings, branch protections, workflows, CI configuration, scripts, product authority, architecture authority, or game work. They do not execute `SYS-PLAN-NEXT-TRANCHE` during this task or select, define, plan, or start Phase 3 work.
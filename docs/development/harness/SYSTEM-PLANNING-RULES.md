# System Planning Rules

## Purpose

This document defines the repository-native planning transition that replenishes a future phase task tranche after normal ready-task selection is exhausted. It preserves the one-task, one-pull-request, human-review, and human-merge model while allowing a later `Proceed with next task.` instruction to select bounded phase planning from an approved roadmap.

## System Transition Identity

- **Transition ID:** `SYS-PLAN-NEXT-TRANCHE`
- **Type:** system planning transition
- **Nature:** planning authority only; not implementation work and not an ordinary phase task
- **Authority:** `PHASE-ROADMAP.md`, `TASK-ELIGIBILITY-AND-COMPLETION-RULES.md`, `TASK-REPLENISHMENT-AND-QUEUE-EXHAUSTION-RULES.md`, `HARNESS-CONTROL-BOUNDARY.md`, and the selected roadmap entry's approved source authority

The transition does not activate a later phase, begin implementation, or select any future task by itself. It may only create a bounded planning PR as specified below.

## Eligibility Trigger Conditions

`SYS-PLAN-NEXT-TRANCHE` is eligible only when every condition is true:

1. No valid harness PR is open.
2. No harness task is active or awaiting human review.
3. No active phase has a ready executable task.
4. The most recent active phase closed through its qualifying merged gate, or no active phase exists.
5. `PHASE-ROADMAP.md` identifies exactly one next phase in state `ready_for_planning`.
6. That roadmap entry identifies phase ID, title, bounded purpose, approved source-authority documents, allowed planning boundary, prohibited scope, and work classification.
7. Every listed source-authority document exists and is sufficiently specific to derive bounded tasks without inventing product, architecture, contract, or game behavior.
8. No unresolved authority conflict blocks planning.

Failure of any condition is a controlled stop. The harness must report the smallest missing roadmap, product, architecture, contract, source-authority, or Project Owner decision and must not create a planning branch or PR.

## Selection Order

On an explicit `Proceed with next task.` instruction, the harness must:

1. Refresh protected-default-branch state and current GitHub pull-request evidence.
2. Derive normal active-phase and task eligibility under `TASK-ELIGIBILITY-AND-COMPLETION-RULES.md`.
3. Select the single lowest normal ready task when one exists.
4. Only when no normal ready task exists, evaluate `SYS-PLAN-NEXT-TRANCHE` against every trigger condition.
5. Select the system transition only when it is the sole eligible planning transition.
6. Otherwise enter the controlled stop state and report the exact missing authority.

Normal ready-task selection always has priority. A system transition cannot run while a valid harness PR is open, while a task is active or awaiting review, or when an active phase has a ready task.

## Authorized Planner Output

When selected, `SYS-PLAN-NEXT-TRANCHE` may create exactly one planning PR for the one roadmap phase that satisfied the trigger conditions. That PR may contain only:

1. one next-phase task register;
2. three to five complete executable task-definition files;
3. one complete qualifying gate definition; and
4. planning and task-authority artifacts required to make that register and definitions executable.

Every generated executable definition must satisfy `EXECUTABLE-TASK-DEFINITION-FORMAT.md` before the planning PR opens, including Task-state authority before Purpose. The planner must validate every required metadata field and narrative section, exact allowed paths, forbidden scope, authority documents, deliverable, acceptance criteria, validation, stop condition, and later-task boundary.

The planner must limit each generated task and gate to the roadmap entry's bounded purpose, source authority, allowed planning boundary, prohibited scope, and work classification. It must not create an unbounded backlog.

## Prohibited Planner Actions

The planner must not:

- create or modify implementation code;
- configure GitHub settings, branch protection, CI, workflows, or scripts;
- invent phase purpose, product behavior, architecture, contracts, or acceptance criteria beyond approved source authority;
- create Phase 4 or later planning unless the selected roadmap entry expressly authorizes it;
- select, draft, pre-stage, or begin any task created by its own planning PR; or
- approve, merge, enable auto-merge, or bypass protection for any pull request.

## Planning PR and Stop Boundary

The planning PR must identify the system transition, selected roadmap entry, source authority, generated artifacts, validation of every generated definition, deferred work, and confirmation that no implementation began.

After opening the planning PR, the harness must stop for human review. The planning transition is complete only when that planning PR merges. Human review and squash merge remain required.

## Post-Merge Behavior

After the planning PR merges:

1. The planned phase becomes active only under the register created by that merged planning PR.
2. The next explicit `Proceed with next task.` instruction selects the single lowest eligible executable task in that phase under normal eligibility rules.
3. Standard one-task, one-PR, human-review, and human-merge boundaries remain unchanged.

A planning PR merge does not authorize an implementation task to begin without the later explicit `Proceed with next task.` instruction.

## Scope Boundary

This document does not create a Phase 3 register, Phase 3 task definition, qualifying gate file, implementation work, GitHub enforcement configuration, workflow, CI, script, product authority, architecture authority, or game work. It only defines the standing selection and output boundary for a future planning transition.
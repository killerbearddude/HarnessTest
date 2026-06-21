# Phase 2 Task Register

## Phase Identity

**Phase 2 — Establish Executable Task Authority**

Phase 2 establishes repository-native executable task authority. Its outcome is a task-definition format and a versioned task set that allows a later `Proceed with next task.` instruction to select and execute one approved, eligible task without a new owner-supplied restatement of its scope, paths, deliverables, acceptance criteria, or validation requirements.

## Completion and Execution Authority

GitHub merged-pull-request evidence determines completed task state. Exactly one harness task may be executing or awaiting human review at any time.

P2-T01 is the Phase 2 setup task. It is complete only when its pull request merges. After P2-T01 merges, a later explicit `Proceed with next task.` instruction is sufficient to authorize execution of the one next eligible Phase 2 task defined in this register and its executable task-definition file.

## Approved Phase 2 Sequence

| Sequence | Task ID | Title | Executable authority |
| --- | --- | --- | --- |
| 1 | P2-T01 | Create the Phase 2 executable task authority set | This setup task; complete only when its PR merges |
| 2 | P2-T02 | Define executable task-definition format | `docs/development/harness/tasks/P2-T02.md` |
| 3 | P2-T03 | Define task eligibility and completion derivation rules | `docs/development/harness/tasks/P2-T03.md` |
| 4 | P2-T04 | Define rolling task-replenishment and queue-exhaustion rules | `docs/development/harness/tasks/P2-T04.md` |
| 5 | P2-GATE-01 | Review and close Phase 2 | `docs/development/harness/tasks/P2-GATE-01.md` |

```text
P2-T01 → P2-T02 → P2-T03 → P2-T04 → P2-GATE-01
```

## Executable Task Definitions

Each remaining Phase 2 task has a separate executable task-definition file under `docs/development/harness/tasks/`. Those files provide the bounded paths, authority documents, deliverables, acceptance criteria, validation, and stop conditions required for execution.

A task is eligible only when its predecessor is completed by merged-PR evidence, the task is in the active phase, no other harness task is executing or awaiting human review, and its executable authority is complete.

## Phase 3 Lock

**Phase 3 remains locked.** It has no authorized tasks, task register, executable task definition, scope, implementation plan, or deliverable.

## Stop Condition

After one PR for the active Phase 2 task is opened, the harness must stop. No later task may be selected or started until the active task's PR merges and a later explicit `Proceed with next task.` instruction is received.
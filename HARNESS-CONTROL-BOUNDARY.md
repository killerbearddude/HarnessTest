# Harness Control Boundary

**Document ID:** HARNESS-POLICY-001  
**Status:** Proposed — effective when merged to the protected default branch  
**Owner:** Project Owner  
**Scope:** Autonomous development-harness operating boundary  
**Applies to:** All harness-driven task selection, system planning, validation, review, branch, and pull-request activity

---

## 1. Purpose

This document defines the operating boundary for the project development harness. The harness advances the repository through small, reviewable units while preserving human control over project direction, architecture, approval, merge decisions, and implementation authority.

The operating loop is:

1. The Project Owner instructs the harness to proceed.
2. The harness selects at most one normal eligible task; only when no normal task is ready, it may select the single eligible roadmap-planning transition.
3. The harness performs that one bounded unit.
4. The harness validates and internally reviews it.
5. The harness opens at most one pull request.
6. The harness stops.
7. A human reviews and squash-merges the pull request.
8. The next Project Owner proceed instruction is required before another selection.

A merged PR is completion evidence. It is not authorization to begin another ordinary task. A merged planning PR only activates its planned phase under its merged register; it still requires a later explicit `Proceed with next task.` before an executable task in that phase may be selected.

---

## 2. Core Control Rules

The following rules are mandatory:

1. Only one harness work unit may be active, and only one valid harness PR may be open, at a time.
2. The harness must stop after opening a PR.
3. The harness must not merge, approve, self-approve, enable auto-merge, or otherwise finalize a PR.
4. The Project Owner remains the final approval authority for every PR and phase gate.
5. The protected remote default branch and current GitHub PR state are authoritative repository state.
6. The harness must not push directly to protected `main`, bypass protection, or force-push a shared or protected branch.
7. The harness must not begin implementation outside an approved executable task in an authorized active phase.
8. A phase closes only through its qualifying merged gate under `TASK-ELIGIBILITY-AND-COMPLETION-RULES.md`.
9. A later phase is not activated by a gate attempt, empty queue, or stale prose; it becomes active only under a merged phase register.
10. System planning may occur only through an eligible `SYS-PLAN-NEXT-TRANCHE` transition governed by `SYSTEM-PLANNING-RULES.md` and `PHASE-ROADMAP.md`.
11. The harness must not invent product, architecture, contract, game-design, evaluator, content, diagnostics, persistence, UI, or implementation behavior.

---

## 3. Authority Order

When information conflicts, the harness must use this precedence order:

1. Explicit current instruction from the Project Owner.
2. GitHub branch protection, required reviews, required checks, and repository access controls.
3. Approved project design documents and approved contracts.
4. The applicable phase register, qualifying-gate state, and approved phase roadmap.
5. `SYSTEM-PLANNING-RULES.md` for the system transition.
6. The active executable task definition, including scope and acceptance criteria.
7. Current protected default-branch state and GitHub PR state.
8. Repository tests, CI configuration, and validation scripts.
9. Local working-tree state.
10. Chat history, summaries, notes, and uncommitted assumptions.

The harness must stop and report a conflict when higher-authority sources disagree. It must not resolve conflict by inventing behavior.

---

## 4. Explicit Commands

### 4.1 Proceed Command

An instruction such as:

```text
Proceed with next task.
```

authorizes the harness to synchronize protected-default-branch state, inspect GitHub PR and CI state, derive normal task eligibility, and select exactly one bounded work unit.

Selection priority is mandatory:

1. Select the single lowest eligible normal executable task when one exists.
2. Only when no normal task is ready, evaluate `SYS-PLAN-NEXT-TRANCHE`.
3. Select the system transition only when every trigger in `SYSTEM-PLANNING-RULES.md` passes and `PHASE-ROADMAP.md` identifies exactly one phase `ready_for_planning`.
4. Otherwise stop and report the smallest missing roadmap, source authority, product, architecture, contract, or Project Owner decision.

A proceed command does not authorize multiple tasks, concurrent work, automatic implementation, scope expansion, planning for a locked phase, merge or approval activity, or speculative work.

### 4.2 Review Command

A review command authorizes read-only review of the currently open harness PR. It does not authorize new work, commits, task selection, planning, merge, approval, or phase advancement.

### 4.3 No Implied Proceeding

A merged PR, GitHub approval, positive review, idle period, prior conversation, empty queue, or absence of objections does not authorize another normal task. Only a later explicit proceed command permits selection.

---

## 5. One-Work-Unit-at-a-Time Rule

The harness may be in only one of these states:

| State | Meaning |
| --- | --- |
| Idle | No active normal task, system transition, or open harness PR. |
| Executing | One selected normal task or system transition is being performed. |
| Awaiting Human Review | One harness PR is open. |
| Blocked | No safe selection is available under current authority. |
| Phase Gate Pending | A qualifying phase-gate PR is awaiting human review. |

The harness must not begin another task, system transition, repair, implementation, or review change while Executing, Awaiting Human Review, Blocked, or Phase Gate Pending.

An open valid harness PR or an open PR with missing or conflicting harness identity blocks all selection.

---

## 6. Bounded Autonomous Actions

Within the scope of the selected normal task or eligible system transition, the harness may inspect repository and GitHub state, create one branch, edit only authorized paths, run permitted validation, perform internal review, and open one PR.

For `SYS-PLAN-NEXT-TRANCHE`, the only additional authority is the bounded planning output in `SYSTEM-PLANNING-RULES.md`: one next-phase register, three to five complete task definitions, one qualifying gate definition, and necessary planning authority artifacts. The system transition may not create implementation or select a task it generates.

---

## 7. Human Decision and Controlled-Stop Boundary

The harness must stop and report the blocker when a PR opens; a required authority document is missing, contradictory, incomplete, or unclear; a task exceeds allowed paths; validation cannot pass inside approved scope; a valid PR already exists; roadmap eligibility is absent or ambiguous; source authority is insufficient; repository state is stale or conflicted; or a new product, architecture, contract, or strategic decision is required.

A completed phase is not by itself a stop when `SYS-PLAN-NEXT-TRANCHE` is eligible. A completed or empty phase with no eligible system transition remains a controlled stop.

When stopped, the harness must report the active or most-recent phase, active task/PR if any, exact blocker, repository evidence, the smallest required decision or authority, and work it did not perform.

---

## 8. Prohibited Actions

The harness must never merge, approve, self-approve, bypass branch protection, push directly to protected `main`, force-push a shared/protected branch, begin a second unit while a PR is open, select a task from a locked or unplanned phase, treat an unmerged branch as completed work, treat chat memory as authoritative repository state, expand scope, hide failed validation, or invent unapproved strategic/domain behavior.

The harness must not configure GitHub settings, branch protection, workflows, CI, scripts, or implementation unless an approved executable task explicitly authorizes that exact work.

---

## 9. Scope, Validation, and PR Boundary

Every ordinary executable task must define task ID, phase, purpose, allowed paths, forbidden scope, authority documents, deliverable, acceptance criteria, validation, stop condition, and later-task boundary. The harness may modify only allowed paths and must not broaden scope during execution.

Before opening a PR, the selected unit must meet its acceptance criteria, required validation, allowed-path boundary, authority requirements, and internal review. Its PR must identify the selected task or system transition, objective, authority, changed and intentionally unchanged files, validation outcomes, known limitations, internal-review result, and the requirement for human review and squash merge.

Every PR must state: `No additional task has been selected or started.`

---

## 10. Phase and Roadmap Boundary Rules

A phase is a bounded set of tasks with entry criteria, exit criteria, and a qualifying gate. The harness executes ordinary tasks only in an active phase under its merged register.

A phase is complete only through its qualifying gate. A qualifying gate merge does not authorize implementation or select a later phase task.

`PHASE-ROADMAP.md` may identify a phase as `ready_for_planning` only when its bounded purpose, source authority, planning boundary, prohibited scope, and work classification are approved. A roadmap entry does not create a phase register or implementation authority.

`SYS-PLAN-NEXT-TRANCHE` may turn exactly one qualifying roadmap entry into a reviewable planning PR. Only after that PR merges does its register govern normal task selection in the planned phase. A later explicit proceed command remains required.

---

## 11. Enforcement and Reporting

For every proceed command, the harness must report protected-default-branch state, open harness PRs, active/closed phase state, ordinary ready-task result, system-planning evaluation when normal readiness is empty, the selected unit if any, eligibility basis, blocking conditions, and stop condition.

For every PR, the harness must state that no additional task was selected or started.

---

## 12. Effective Policy Statement

This harness is a controlled executor with a bounded roadmap-driven planning transition. It is not an autonomous project owner. It may execute only approved tasks and, when normal work is exhausted, only the explicitly constrained system planner backed by an approved roadmap and specific source authority. Human review and squash merge remain required for every PR.
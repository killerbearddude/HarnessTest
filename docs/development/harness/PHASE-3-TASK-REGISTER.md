# Phase 3 Task Register

## Phase Identity

- **Phase ID:** Phase 3
- **Title:** Implement Repository Enforcement
- **Work classification:** Governance
- **Planning authority:** `SYS-PLAN-NEXT-TRANCHE`, selected from the sole `ready_for_planning` Phase 3 roadmap entry.
- **Activation authority:** This register becomes the active Phase 3 authority only when the planning pull request that introduces it merges into `main`. Current GitHub pull-request evidence controls over static status wording.

## Purpose

Implement and verify the repository-protection and pull-request/CI enforcement required before implementation work may proceed. This phase is limited to repository enforcement. It does not create game, product, architecture, graph-domain, evaluator, content, diagnostics, persistence, or UI work.

## Approved Source Authority

- `docs/development/harness/REPOSITORY-PROTECTION-REQUIREMENTS.md`
- `docs/development/harness/PULL-REQUEST-AND-CI-ENFORCEMENT-REQUIREMENTS.md`
- `HARNESS-CONTROL-BOUNDARY.md`
- `docs/development/harness/TASK-ELIGIBILITY-AND-COMPLETION-RULES.md`
- `docs/development/harness/TASK-REPLENISHMENT-AND-QUEUE-EXHAUSTION-RULES.md`
- `docs/development/harness/EXECUTABLE-TASK-DEFINITION-FORMAT.md`
- This register and the Phase 3 executable task definitions listed below.

## Planned State and Normal Selection

Before the Phase 3 planning PR merges, Phase 3 is `planned` and no Phase 3 task may be selected. After that PR merges, Phase 3 is active under this register.

After activation, a later explicit `Proceed with next task.` instruction may select only the lowest ready Phase 3 task. P3-T01 is the sole initial ready task. P3-T02, P3-T03, and P3-GATE-01 remain blocked until their direct predecessors have merged.

## Approved Sequence

| Sequence | Task ID | Title | Executable authority |
| --- | --- | --- | --- |
| 1 | P3-T01 | Implement pull-request and CI enforcement | `docs/development/harness/tasks/P3-T01.md` |
| 2 | P3-T02 | Configure protected default-branch enforcement | `docs/development/harness/tasks/P3-T02.md` |
| 3 | P3-T03 | Verify repository-enforcement requirements | `docs/development/harness/tasks/P3-T03.md` |
| 4 | P3-GATE-01 | Review and close Phase 3 | `docs/development/harness/tasks/P3-GATE-01.md` |

```text
P3-T01 → P3-T02 → P3-T03 → P3-GATE-01
```

## Qualifying Gate Authority

P3-GATE-01 is the only qualifying Phase 3 closure gate. Phase 3 closes only when:

1. P3-T01 through P3-T03 have merged completion evidence;
2. P3-GATE-01 is the register-designated qualifying gate;
3. its gate report records every required closure criterion as Pass;
4. its report explicitly recommends Phase 3 closure; and
5. its qualifying gate PR merges.

A merged gate attempt with any Fail or Blocked criterion does not close Phase 3 or authorize any later phase.

## Phase Boundary

Phase 4 and later phases remain locked. This register does not authorize Phase 4 planning, product authority, architecture authority, game work, or implementation outside the repository-enforcement scope of this phase.

## Stop Condition

After a PR for the current Phase 3 task is opened, the harness must stop. No later task may be selected or started until that PR merges and a later explicit `Proceed with next task.` instruction is received.
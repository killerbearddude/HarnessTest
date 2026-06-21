# Phase 1 Task Register

## Phase Identity and Boundary

**Phase 1 — Establish Repository Enforcement**

This register is the authoritative Phase 1 task-control record. Phase 1 establishes repository-enforcement requirements for the harness. This register defines task sequence and boundaries only; it does not configure GitHub, CI, workflows, scripts, or branch protections.

## Completion and Execution Authority

GitHub merged-pull-request evidence is the authority for task completion. Exactly one Phase 1 task may be active or awaiting review at a time.

A later task becomes eligible only when its direct predecessor has merged and a later explicit `Proceed with next task.` instruction is given. An open PR means the represented task is awaiting review and blocks selection or execution of any successor.

## Approved Phase 1 Sequence

| Sequence | Task ID | Title | Initial status |
| --- | --- | --- | --- |
| 1 | P1-T01 | Define the Phase 1 Task Register | Current authorized task |
| 2 | P1-T02 | Define Repository Protection Requirements | Later task; eligible only after P1-T01 merges and a later `Proceed with next task.` instruction |
| 3 | P1-T03 | Define Pull Request and CI Enforcement Requirements | Later task; eligible only after P1-T02 merges and a later `Proceed with next task.` instruction |
| 4 | P1-GATE-01 | Review and Close Phase 1 | Later phase gate; eligible only after P1-T03 merges and a later `Proceed with next task.` instruction |

```text
P1-T01 → P1-T02 → P1-T03 → P1-GATE-01
```

## Task Definitions

### P1-T01 — Define the Phase 1 Task Register

- **Executable scope:** Create and maintain this authoritative Phase 1 task register only.
- **Deliverable:** `docs/development/harness/PHASE-1-TASK-REGISTER.md`.
- **Acceptance conditions:** The register defines only P1-T01, P1-T02, P1-T03, and P1-GATE-01; establishes their dependencies and eligibility conditions; identifies merged PR evidence as completion authority; preserves one-task-at-a-time operation; and locks Phase 2.

### P1-T02 — Define Repository Protection Requirements

- **Executable scope:** Define repository-protection requirements for harness enforcement. No GitHub settings or protections are configured by this task definition.
- **Deliverable:** A bounded requirements document authorized when P1-T02 becomes eligible.
- **Acceptance conditions:** Requirements identify the repository-protection outcomes and verification evidence needed for later implementation, remain limited to repository enforcement, and do not change repository settings, workflows, CI, scripts, game code, or product authority.

### P1-T03 — Define Pull Request and CI Enforcement Requirements

- **Executable scope:** Define pull-request and CI enforcement requirements for harness enforcement. No workflow, CI, script, or GitHub configuration is created by this task definition.
- **Deliverable:** A bounded requirements document authorized when P1-T03 becomes eligible.
- **Acceptance conditions:** Requirements identify pull-request and CI enforcement outcomes and verification evidence needed for later implementation, remain limited to repository enforcement, and do not change repository settings, workflows, CI, scripts, game code, or product authority.

### P1-GATE-01 — Review and Close Phase 1

- **Executable scope:** Review Phase 1 completion evidence and determine whether its defined repository-enforcement requirements are complete and ready for closure.
- **Deliverable:** A Phase 1 gate report and any necessary Phase 1 register update, both authorized only when P1-GATE-01 becomes eligible.
- **Acceptance conditions:** The gate records merged-PR evidence for P1-T01 through P1-T03, evaluates Phase 1 criteria, states that closure is contingent on the gate PR merge, and does not define or start Phase 2 work.

## Locked Scope

This register does not authorize:

- game code;
- product or game-design documents;
- evaluator, content, diagnostics, persistence, or UI contracts;
- GitHub workflows, CI configuration, harness scripts, or branch-protection changes;
- Phase 2 or later task definitions; or
- selection, planning, or execution of P1-T02, P1-T03, P1-GATE-01, or later-phase work before eligibility conditions are met.

## Phase 2 Lock

**Phase 2 remains locked.** It has no authorized tasks. Phase 1 completion does not authorize Phase 2 setup, task definition, planning, or execution.

## Stop Condition

After one PR for the active Phase 1 task is opened, the harness must stop. No successor task may be selected or started until its predecessor has merged and a later explicit `Proceed with next task.` instruction is given.

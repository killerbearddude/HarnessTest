# Executable Task Definition: P3-GATE-01

## Task Identity

- **Task ID:** P3-GATE-01
- **Phase:** Phase 3 — Implement Repository Enforcement
- **Title:** Review and close Phase 3
- **Task type:** qualifying phase gate
- **Predecessor dependency:** P3-T03 must be completed by merged pull-request evidence.
- **Task-state authority:** GitHub merged pull-request evidence determines predecessor completion; P3-T03 must be merged before P3-GATE-01 may become ready. GitHub open pull-request evidence determines whether a harness task is active or awaiting human review. The merged Phase 3 register identifies P3-GATE-01 as the sole qualifying closure gate; Phase 3 closes only when the P3-GATE-01 report records every required closure criterion as Pass, explicitly recommends closure, and the qualifying gate PR merges. This P3-GATE-01 definition governs scope, deliverable, acceptance criteria, validation, and stop condition. Current GitHub PR evidence controls over stale static task-status wording. A missing or invalid required task-definition field blocks execution. Exactly one harness task or planning PR may be executing or awaiting human review at a time.

## Purpose

Re-evaluate Phase 3 repository-enforcement evidence and close Phase 3 only if every required repository-protection and pull-request/CI enforcement criterion passes. The gate does not create later-phase authority or authorize implementation work.

## Allowed Paths

- `docs/development/harness/PHASE-3-GATE-REPORT.md`
- `docs/development/harness/PHASE-3-TASK-REGISTER.md`

## Forbidden Scope

No game code; product, architecture, graph-domain, evaluator, content, diagnostics, persistence, or UI work; GitHub settings changes; branch-protection changes; workflow, CI, script, or repository configuration changes; Phase 4 task definitions or planning; or changes outside the allowed paths are authorized.

## Required Authority Documents

- `docs/development/harness/PHASE-3-TASK-REGISTER.md`
- `docs/development/harness/tasks/P3-GATE-01.md`
- `docs/development/harness/tasks/P3-T01.md`
- `docs/development/harness/tasks/P3-T02.md`
- `docs/development/harness/tasks/P3-T03.md`
- `docs/development/harness/PHASE-3-ENFORCEMENT-VERIFICATION.md`
- `docs/development/harness/REPOSITORY-PROTECTION-REQUIREMENTS.md`
- `docs/development/harness/PULL-REQUEST-AND-CI-ENFORCEMENT-REQUIREMENTS.md`
- `HARNESS-CONTROL-BOUNDARY.md`
- `docs/development/harness/TASK-ELIGIBILITY-AND-COMPLETION-RULES.md`

## Required Deliverable

1. Create or update `docs/development/harness/PHASE-3-GATE-REPORT.md`.
2. Re-evaluate every Phase 3 closure criterion using merged evidence for P3-T01 through P3-T03 and current repository evidence.
3. Verify that the P3-T03 enforcement-verification report covers every required enforcement category and that any Fail or Blocked finding is reflected in the gate result.
4. Record every closure criterion as Pass, Fail, or Blocked with evidence.
5. Recommend Phase 3 closure only when every required criterion is Pass.
6. Update the Phase 3 register only as necessary to record the qualifying gate status, preserving that closure is effective only after this gate PR merges.
7. Keep Phase 4 and later phases locked and undefined.

## Acceptance Criteria

- The gate report records all Phase 3 closure criteria as Pass, Fail, or Blocked with specific evidence.
- The gate report evaluates each repository-protection and pull-request/CI enforcement requirement.
- A closure recommendation appears only when every required criterion is Pass.
- The register identifies P3-GATE-01 as the qualifying closure gate and does not state that Phase 3 is closed while this gate PR is open.
- Phase 4 remains locked and undefined.
- No file outside the allowed paths changes.

## Required Validation

- Inspect merged evidence for P3-T01, P3-T02, and P3-T03.
- Inspect the current P3-T03 verification report, source enforcement requirements, Phase 3 register, and current GitHub configuration/check evidence needed to confirm report consistency.
- Confirm every required gate criterion is recorded with evidence.
- Confirm only the allowed paths changed.
- Runtime game, product, architecture, and UI validation are intentionally not applicable and not authorized.

## Stop Condition

Open one reviewable P3-GATE-01 pull request and stop. Await human review and merged GitHub evidence. Do not approve, merge, enable auto-merge, or claim Phase 3 closure before the qualifying merged evidence exists.

## Later-Task Boundary

This task cannot select, define, plan, or start Phase 4 or later work, product work, architecture work, or game implementation.
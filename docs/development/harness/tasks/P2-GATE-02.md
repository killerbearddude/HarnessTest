# Executable Task Definition: P2-GATE-02

## Task Identity

- **Task ID:** P2-GATE-02
- **Phase:** Phase 2 — Establish Executable Task Authority
- **Title:** Re-review and close Phase 2
- **Task type:** qualifying phase gate
- **Predecessor dependency:** P2-R04 must be completed by merged pull-request evidence.
- **Task-state authority:** GitHub merged pull-request evidence determines predecessor completion; P2-R04 must be merged before P2-GATE-02 may become ready. GitHub open pull-request evidence determines whether a harness task is active or awaiting human review. The active Phase 2 register identifies P2-GATE-02 as the sole qualifying closure gate, and merged qualifying-gate evidence determines Phase 2 closure only when its gate report records every required closure criterion as Pass and explicitly recommends closure. This P2-GATE-02 task-definition file governs P2-GATE-02 scope, deliverable, acceptance criteria, validation, and stop condition. Current GitHub PR evidence controls over stale static task-status wording. A missing or invalid required task-definition field blocks execution. Exactly one harness task may be executing or awaiting human review at a time.

## Purpose

Re-evaluate the complete Phase 2 evidence after P2-R04 and close Phase 2 only if every required closure criterion passes.

## Allowed Paths

- `docs/development/harness/PHASE-2-GATE-REPORT.md`
- `docs/development/harness/PHASE-2-TASK-REGISTER.md`

## Forbidden Scope

No game code, GitHub configuration, branch-protection changes, workflows, CI configuration, scripts, Phase 3 task definitions, Phase 3 work, or changes to executable task definitions are authorized.

## Required Authority Documents

- `docs/development/harness/PHASE-2-TASK-REGISTER.md`
- `docs/development/harness/tasks/P2-GATE-02.md`
- `docs/development/harness/tasks/P2-R04.md`
- `docs/development/harness/PHASE-2-GATE-REPORT.md`
- `docs/development/harness/EXECUTABLE-TASK-DEFINITION-FORMAT.md`
- `docs/development/harness/TASK-ELIGIBILITY-AND-COMPLETION-RULES.md`
- `docs/development/harness/TASK-REPLENISHMENT-AND-QUEUE-EXHAUSTION-RULES.md`
- `docs/development/harness/REPOSITORY-PROTECTION-REQUIREMENTS.md`
- `docs/development/harness/PULL-REQUEST-AND-CI-ENFORCEMENT-REQUIREMENTS.md`

## Required Deliverable

1. Re-evaluate every Phase 2 closure criterion.
2. Verify P2-T02 has complete executable authority.
3. Verify P2-T04 replenishment rules are unambiguous and consistent with qualifying-gate lifecycle semantics.
4. Record every criterion as Pass, Fail, or Blocked.
5. Recommend Phase 2 closure only when every required criterion is Pass.
6. State that Phase 2 closes only when this qualifying P2-GATE-02 pull request merges.
7. Keep Phase 3 locked and undefined.

## Acceptance Criteria

- The report evaluates every required closure criterion with Pass, Fail, or Blocked evidence.
- P2-T02 compliance and P2-T04 replenishment clarity are explicitly evaluated.
- A closure recommendation appears only if every required criterion is Pass.
- The register identifies P2-GATE-02 as the qualifying closure gate and records Phase 2 closure only after its qualifying PR merges.
- Phase 3 remains locked and undefined.
- No file outside the allowed paths changes.

## Required Validation

- Inspect merged evidence for all required Phase 2 tasks and P2-R04.
- Inspect every required authority document for cross-document consistency.
- Confirm the changed-file set contains only the allowed paths.
- Record every gate criterion and its evidence in the report.
- Runtime, repository-configuration, CI, workflow, and script validation are not required or authorized for this documentation gate.

## Stop Condition

Open one reviewable P2-GATE-02 PR and stop. Await human review and merge. Do not approve, merge, or claim Phase 2 closure before qualifying merged GitHub evidence exists.

## Later-Task Boundary

This task cannot select, define, plan, or start Phase 3 or any later work.

# Executable Task Definition: P2-GATE-01

## Task Identity

- **Task ID:** P2-GATE-01
- **Phase:** Phase 2 — Establish Executable Task Authority
- **Title:** Review and close Phase 2
- **Task type:** phase gate
- **Predecessor dependency:** P2-T04 must be completed by merged pull-request evidence.
- **Task-state authority:** GitHub merged pull-request evidence determines predecessor completion; P2-T04 must be merged before P2-GATE-01 may become ready. GitHub open pull-request evidence determines whether a harness task is active or awaiting human review. The active Phase 2 register and merged phase-gate evidence determine active-phase status. This P2-GATE-01 task-definition file governs P2-GATE-01 scope, deliverable, acceptance criteria, validation, and stop condition. Current GitHub PR evidence controls over stale static task-status wording. A missing or invalid required task-definition field blocks execution. Exactly one harness task may be executing or awaiting human review at a time.

## Purpose

Review Phase 2 merged evidence and determine whether Phase 2 established executable task authority sufficient for later tasks to run without a new owner-supplied scope prompt.

## Allowed Paths

- `docs/development/harness/PHASE-2-GATE-REPORT.md`
- `docs/development/harness/PHASE-2-TASK-REGISTER.md`

## Forbidden Scope

No code, repository settings, branch-protection changes, workflows, CI configuration, scripts, product or design documents, Phase 3 or later task definitions, or changes to `docs/development/harness/tasks/` are authorized.

## Required Authority Documents

- `docs/development/harness/PHASE-2-TASK-REGISTER.md`
- `docs/development/harness/tasks/P2-GATE-01.md`
- `docs/development/harness/tasks/P2-T02.md`
- `docs/development/harness/tasks/P2-T03.md`
- `docs/development/harness/tasks/P2-T04.md`
- `docs/development/harness/EXECUTABLE-TASK-DEFINITION-FORMAT.md`
- `docs/development/harness/TASK-ELIGIBILITY-AND-COMPLETION-RULES.md`
- `docs/development/harness/TASK-REPLENISHMENT-AND-QUEUE-EXHAUSTION-RULES.md`
- `docs/development/harness/REPOSITORY-PROTECTION-REQUIREMENTS.md`
- `docs/development/harness/PULL-REQUEST-AND-CI-ENFORCEMENT-REQUIREMENTS.md`

## Required Deliverable

Create `docs/development/harness/PHASE-2-GATE-REPORT.md` and update the Phase 2 register only as necessary to record gate-review status and closure after the gate PR merges.

The report must:

- review merged evidence for P2-T01 through P2-T04;
- verify that P2-T02 through P2-T04 each had complete executable authority sufficient to execute without a manual scope prompt;
- verify that the executable task-definition format, eligibility/completion rules, and replenishment/queue-exhaustion rules are consistent;
- record each gate criterion as Pass, Fail, or Blocked with brief evidence;
- state whether the evidence supports closing Phase 2;
- state that Phase 2 closure becomes effective only when the gate PR merges; and
- state that Phase 3 remains locked and has no authorized work.

## Acceptance Criteria

- The report records merged PR evidence for P2-T01 through P2-T04.
- The report evaluates executable-authority completeness, rule consistency, and Phase 2 scope boundaries.
- Every gate criterion has an explicit Pass, Fail, or Blocked result.
- The register records P2-T01 through P2-T04 completion from merged evidence and marks the gate awaiting human review until merged.
- The register states that the gate PR merge is the only Phase 2 closure event.
- Neither report nor register defines Phase 3 tasks, scope, or work.
- No file outside the allowed paths changes.

## Required Validation

- Inspect merged evidence for P2-T01 through P2-T04.
- Inspect each required authority document for the required content and cross-document consistency.
- Confirm the changed-file set contains only the allowed paths.
- Record every gate criterion result with its evidence in the report.
- No repository configuration, CI, workflow, or script validation is authorized for this documentation gate.

## Stop Condition

Open one reviewable gate PR and stop. Await human review and merge. Do not approve, merge, or declare Phase 2 closed before merged GitHub evidence for the gate PR exists.

## Later-Task Boundary

This task cannot select, define, plan, or start any Phase 3 work.

# Executable Task Definition: TEMPLATE-GATE-01

## Task Identity

- **Task ID:** TEMPLATE-GATE-01
- **Phase:** Generic Template Conversion
- **Title:** Review template readiness and close the conversion phase
- **Task type:** qualifying gate
- **Predecessor dependency:** TEMPLATE-T03 must have exact merged pull-request evidence.
- **Task-state authority:** GitHub merged evidence for TEMPLATE-T03 is required. The active conversion register must designate TEMPLATE-GATE-01 as the sole qualifying gate, no exact merged TEMPLATE-GATE-01 evidence may exist, and no valid harness PR or active task may exist. The conversion phase closes only when this gate's report records every criterion as Pass, explicitly recommends closure, and its PR merges.
- **Source-authority documents:** `docs/template/TEMPLATE-CONVERSION-REGISTER.md`; `docs/template/TEMPLATE-CHARTER.md`; `docs/template/PROJECT-BOOTSTRAP.md`; `docs/template/PHASE-ROADMAP-TEMPLATE.md`; `docs/template/TASK-CATALOG-TEMPLATE.md`; `docs/template/EXECUTABLE-TASK-DEFINITION-TEMPLATE.md`; `docs/template/EXTERNAL-CONTROL-CHECKLIST.md`
- **Active register:** `docs/template/TEMPLATE-CONVERSION-REGISTER.md`

## Purpose

Evaluate generic template readiness and close the template-conversion phase only when every required template-control and source-backed-planning criterion passes.

## Allowed Paths

- `docs/template/TEMPLATE-CONVERSION-GATE-REPORT.md`
- `docs/template/TEMPLATE-CONVERSION-REGISTER.md`

## Forbidden Scope

Project-specific implementation, source documents, task catalogs, external GitHub administration, workflows, CI, scripts, and future project phases are forbidden.

## Required Deliverable

Create `docs/template/TEMPLATE-CONVERSION-GATE-REPORT.md` with a Pass, Fail, or Blocked result and evidence for template charter, bootstrap, source-manifest workflow, roadmap template, catalog template, executable-definition template, horizon validation, external-control boundary, pilot retirement treatment, and generic identity handling.

## Acceptance Criteria

- Every required readiness criterion is recorded as Pass, Fail, or Blocked with evidence.
- The report recommends conversion closure only when every criterion is Pass.
- The register is updated only to record gate status and must not state closure while the gate PR is open.
- No project-specific authority or implementation work is created.

## Required Validation

- Confirm exact merged evidence for TEMPLATE-T01 through TEMPLATE-T03.
- Confirm the report covers every required template artifact and external-control boundary.
- Confirm only allowed paths changed.
- Confirm no current project implementation phase is activated.

## Stop Condition

Open one reviewable TEMPLATE-GATE-01 PR and stop. Do not approve, merge, enable auto-merge, or claim conversion closure before exact merged gate evidence exists.

## Later-Task Boundary

Do not define, select, plan, or start any future project task, implementation phase, external-control change, or project-specific work.
# Executable Task Definition: TEMPLATE-T03

## Task Identity

- **Task ID:** TEMPLATE-T03
- **Phase:** Generic Template Conversion
- **Title:** Implement generic task-catalog and executable-horizon validation
- **Task type:** template validation implementation
- **Predecessor dependency:** TEMPLATE-T02 must have exact merged pull-request evidence.
- **Task-state authority:** GitHub merged evidence for TEMPLATE-T02 is required. The active conversion register must list TEMPLATE-T03 in the executable horizon, no exact merged TEMPLATE-T03 evidence may exist, and no valid harness PR or active task may exist. This definition governs scope, validation, and stop condition.
- **Source-authority documents:** `docs/template/TASK-CATALOG-TEMPLATE.md`; `docs/template/EXECUTABLE-TASK-DEFINITION-TEMPLATE.md`; `docs/template/PROJECT-BOOTSTRAP.md`; `docs/template/TEMPLATE-CONVERSION-REGISTER.md`
- **Active register:** `docs/template/TEMPLATE-CONVERSION-REGISTER.md`

## Purpose

Implement generic repository-native validation artifacts that verify a catalog-backed executable horizon has complete definitions, explicit source authority, and a qualifying gate without hard-coding any project's phase names or product domain.

## Allowed Paths

- `docs/template/TASK-CATALOG-TEMPLATE.md`
- `docs/template/EXECUTABLE-TASK-DEFINITION-TEMPLATE.md`
- `docs/template/EXECUTABLE-HORIZON-VALIDATION.md`
- `.github/workflows/harness-pr-evidence.yml`

## Forbidden Scope

Project-specific catalog entries, source documents, implementation work, external GitHub settings, scripts, unrelated workflows, and future conversion tasks are forbidden.

## Required Deliverable

Create `docs/template/EXECUTABLE-HORIZON-VALIDATION.md` and update only allowed template formats or the generic PR-evidence workflow as necessary to validate generic task identity, required definition fields, catalog-to-horizon linkage, and qualifying-gate presence.

## Acceptance Criteria

- Generic task identity validation accepts authority-defined program prefixes and does not hard-code a project phase name.
- The validation artifact distinguishes catalog planning from executable-horizon permission.
- The validation requires three to five complete task definitions and one qualifying gate for a new project horizon.
- No project-specific or external-administration behavior is introduced.

## Required Validation

- Confirm TEMPLATE-T02 exact merged evidence.
- Confirm only allowed paths changed.
- Validate generic task-identity grammar against template examples.
- Validate that required definition fields include Task-state authority before Purpose.
- Confirm no workflow requires a check before a non-`main` feature branch can be created.

## Stop Condition

Open one reviewable TEMPLATE-T03 PR and stop. Do not approve, merge, enable auto-merge, or select a successor task.

## Later-Task Boundary

Do not create a readiness gate report, close the conversion phase, create project-specific authority, configure external settings, or begin TEMPLATE-GATE-01.
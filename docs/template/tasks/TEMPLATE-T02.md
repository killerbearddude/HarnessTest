# Executable Task Definition: TEMPLATE-T02

## Task Identity

- **Task ID:** TEMPLATE-T02
- **Phase:** Generic Template Conversion
- **Title:** Implement generic project-bootstrap and source-manifest artifacts
- **Task type:** template artifact implementation
- **Predecessor dependency:** TEMPLATE-T01 must have exact merged pull-request evidence.
- **Task-state authority:** GitHub merged evidence for TEMPLATE-T01 is required. The active conversion register must list TEMPLATE-T02 in the executable horizon, no exact merged TEMPLATE-T02 evidence may exist, and no valid harness PR or active task may exist. This definition governs scope, validation, and stop condition.
- **Source-authority documents:** `docs/template/PROJECT-BOOTSTRAP.md`; `docs/template/TEMPLATE-CHARTER.md`; `docs/template/TEMPLATE-CONVERSION-REGISTER.md`; `docs/template/EXECUTABLE-TASK-DEFINITION-TEMPLATE.md`
- **Active register:** `docs/template/TEMPLATE-CONVERSION-REGISTER.md`

## Purpose

Add reusable source-manifest artifacts and cross-links so a future project can record approved source authority before it derives a roadmap, catalog, or implementation horizon.

## Allowed Paths

- `docs/template/PROJECT-BOOTSTRAP.md`
- `docs/template/SOURCE-MANIFEST-TEMPLATE.md`
- `docs/template/TEMPLATE-CHARTER.md`

## Forbidden Scope

Project-specific source documents, project roadmaps, task catalogs, implementation work, external GitHub settings, workflows, CI, scripts, and future conversion tasks are forbidden.

## Required Deliverable

Create `docs/template/SOURCE-MANIFEST-TEMPLATE.md` and update only the allowed bootstrap/charter documents as needed to cross-reference it.

## Acceptance Criteria

- The source-manifest template records document ID, path/reference, owner, authority level, approval status, scope, limitation, and reviewed date.
- The bootstrap flow requires manifest-backed authority before roadmap and catalog creation.
- No project-specific source material or implementation authority is added.

## Required Validation

- Confirm TEMPLATE-T01 exact merged evidence.
- Confirm only allowed paths changed.
- Confirm the manifest template and bootstrap workflow require source authority before planning.
- Confirm no project-specific terms or implementation artifacts are introduced.

## Stop Condition

Open one reviewable TEMPLATE-T02 PR and stop. Do not approve, merge, enable auto-merge, or select a successor task.

## Later-Task Boundary

Do not implement catalog-validation artifacts, gate reports, project catalog entries, project tasks, workflows, CI, scripts, external settings, or work for TEMPLATE-T03 or TEMPLATE-GATE-01.
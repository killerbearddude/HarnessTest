# Executable Task Definition: TEMPLATE-T01

## Task Identity

- **Task ID:** TEMPLATE-T01
- **Phase:** Generic Template Conversion
- **Title:** Normalize generic harness core and separate pilot history
- **Task type:** governance and archive normalization
- **Predecessor dependency:** `docs/template/TEMPLATE-CONVERSION-REGISTER.md` must be merged.
- **Task-state authority:** GitHub merged evidence for the introducing template-plan PR activates the conversion register. The register must identify TEMPLATE-T01 as the sole initial ready task. No valid harness PR may be open, no exact merged TEMPLATE-T01 PR may exist, and no other task may be active or awaiting review. The source authority is the template charter, archive map, retirement decision, and active register. This definition governs scope, validation, and stop condition.
- **Source-authority documents:** `docs/template/TEMPLATE-CHARTER.md`; `docs/template/PILOT-ARCHIVE-MAP.md`; `docs/archive/harness-test-pilot/PILOT-RETIREMENT-DECISION.md`; `docs/template/TEMPLATE-CONVERSION-REGISTER.md`
- **Active register:** `docs/template/TEMPLATE-CONVERSION-REGISTER.md`

## Purpose

Normalize generic core documentation and retained pilot-history treatment so no pilot phase remains active authority and the repository is clearly a reusable template.

## Allowed Paths

- `README.md`
- `HARNESS-CONTROL-BOUNDARY.md`
- `docs/template/TEMPLATE-CHARTER.md`
- `docs/template/PILOT-ARCHIVE-MAP.md`
- `docs/archive/harness-test-pilot/**`

## Forbidden Scope

Project-specific source documents, product or implementation work, external GitHub settings, workflows, CI, scripts, current conversion task definitions other than the allowed documents, and future-project planning are forbidden.

## Required Deliverable

A consistency update to the allowed generic core and archive documents that confirms the repository contains no active pilot task authority and no project implementation authority.

## Acceptance Criteria

- The allowed documents consistently identify the repository as a generic template.
- Pilot history remains preserved and is not represented as active authority.
- No project-specific authority or implementation work is introduced.

## Required Validation

- Compare changed files to the exact allowed-path list.
- Confirm active authority remains the template-conversion register.
- Confirm the documents contain no project-specific product, architecture, or implementation content.

## Stop Condition

Open one reviewable TEMPLATE-T01 PR and stop. Do not approve, merge, enable auto-merge, or select a successor task.

## Later-Task Boundary

Do not create source-manifest artifacts, catalog-validation artifacts, gate reports, project-specific plans, external settings, or work for TEMPLATE-T02, TEMPLATE-T03, TEMPLATE-GATE-01, or any future project.
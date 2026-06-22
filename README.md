# Development Harness Template

This repository is a reusable, source-backed development-harness template. It is not an active product repository and contains no current project implementation authority.

## Operating Model

```text
Approved project source documents
  → source manifest
  → phase roadmap
  → full task catalog
  → executable task horizon
  → one-task pull-request loop
```

A project begins by supplying approved source documents. The harness records their authority and status in a source manifest, derives a roadmap and a complete task catalog, then creates only a small executable horizon: three to five fully executable task definitions and one qualifying gate. A later explicit `Proceed with next task.` selects one eligible task, opens one reviewable PR, and stops.

The harness does not invent product direction, architecture, contracts, scope, implementation behavior, or external-control settings not supported by approved source documents and an active authority register.

## Template Entry Points

- `docs/template/TEMPLATE-CHARTER.md` — template purpose and control principles.
- `docs/template/PROJECT-BOOTSTRAP.md` — required source-backed project-start workflow.
- `docs/template/PHASE-ROADMAP-TEMPLATE.md` — roadmap format and state rules.
- `docs/template/TASK-CATALOG-TEMPLATE.md` — long-range task catalog format.
- `docs/template/EXECUTABLE-TASK-DEFINITION-TEMPLATE.md` — executable definition format.
- `docs/template/EXTERNAL-CONTROL-CHECKLIST.md` — manual Project Owner external-control checkpoint.
- `docs/template/TEMPLATE-CONVERSION-REGISTER.md` — active template-conversion authority after its introducing PR merges.
- `docs/template/PILOT-ARCHIVE-MAP.md` — retained pilot-history map.

## Pilot History

Historical pilot material is retained for traceability under its existing paths and through `docs/archive/harness-test-pilot/`. It is not active authority for new projects. Phase 3 pilot work is retired, not treated as completed template work.

## Human Control

The harness never merges, approves, enables auto-merge, bypasses protection, or pushes directly to a protected default branch. Every task uses one branch, one PR, human review, and a later explicit proceed instruction before the next selection.
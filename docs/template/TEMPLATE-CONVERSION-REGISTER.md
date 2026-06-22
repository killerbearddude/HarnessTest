# Template Conversion Register

## Status and Authority

**Status:** Active only after the PR that introduces this register merges.  
**Authority:** Direct Project Owner authorization for `TEMPLATE-PLAN-01`, this register, the generic template documents, and the harness control boundary.

After merge, this register is the active authority for the repository's generic template-conversion phase. The historical P0–P3 pilot sequence is retired history. Phase 3 is not completed template work and may not be selected, resumed, or used as current authority. No project implementation phase is active.

## Conversion Purpose

Convert the repository from a self-hosted pilot history into a generic, reusable, source-backed development-harness template.

## Full Conversion Task Catalog

| task ID | phase | title | purpose | task type | predecessor or dependency | source-authority documents | expected deliverable | primary acceptance outcome | decision dependency, if any | catalog status | executable horizon |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| TEMPLATE-T01 | Generic Template Conversion | Normalize generic harness core and separate pilot history | Make generic controls and retained pilot history unambiguous. | governance and archive normalization | this register merged | template charter, archive map, control boundary | normalized generic core and archive treatment | no pilot phase remains active authority | none | in-horizon | yes |
| TEMPLATE-T02 | Generic Template Conversion | Implement generic project-bootstrap and source-manifest artifacts | Add reusable source-manifest bootstrap support. | template artifact implementation | TEMPLATE-T01 merged | project bootstrap, charter, catalog template | generic source-manifest template and bootstrap cross-check | a future project can manifest source authority before planning | none | in-horizon | yes |
| TEMPLATE-T03 | Generic Template Conversion | Implement generic task-catalog and executable-horizon validation | Add generic validation support for catalog-to-horizon conversion. | template validation implementation | TEMPLATE-T02 merged | catalog template, definition template, control rules | catalog and horizon validation artifacts | only complete catalog-backed tasks enter a horizon | none | in-horizon | yes |
| TEMPLATE-GATE-01 | Generic Template Conversion | Review template readiness and close the conversion phase | Evaluate conversion outputs and close only on Pass evidence. | qualifying gate | TEMPLATE-T03 merged | this register and all template artifacts | readiness gate report | closure recommendation only if every criterion passes | none | in-horizon | yes |

## Executable Horizon

The executable horizon consists only of:

1. `docs/template/tasks/TEMPLATE-T01.md`
2. `docs/template/tasks/TEMPLATE-T02.md`
3. `docs/template/tasks/TEMPLATE-T03.md`
4. `docs/template/tasks/TEMPLATE-GATE-01.md`

After this register merges, `TEMPLATE-T01` is the sole initial ready task. `TEMPLATE-T02`, `TEMPLATE-T03`, and `TEMPLATE-GATE-01` remain blocked by exact predecessor evidence.

## Qualifying Closure

The conversion phase closes only when `TEMPLATE-GATE-01` merges, its report records every required closure criterion as Pass, and it explicitly recommends closure. Retirement of pilot history is not conversion closure.

## Boundary

This register does not authorize project-specific implementation, product design, architecture, external GitHub administration, or a future project's task catalog. It authorizes only the bounded generic template-conversion horizon above.
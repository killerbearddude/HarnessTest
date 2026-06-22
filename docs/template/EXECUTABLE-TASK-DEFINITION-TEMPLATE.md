# Executable Task Definition Template

## Definition Rule

A task is executable only when every required field below is complete, internally consistent, and represented in a merged active register's executable horizon. **Task-state authority must appear before Purpose.**

## Task Identity

- **Task ID:** `<PROGRAM>-T<NN>` or `<PROGRAM>-GATE-<NN>`
- **Phase:** `<active register phase or conversion>`
- **Title:** `<bounded title>`
- **Task type:** `<type>`
- **Predecessor dependency:** `<exact task, decision, or none>`
- **Task-state authority:** `<GitHub completion evidence, register state, source status, decision dependency, and PR lock rule>`
- **Source-authority documents:** `<source-manifest IDs and repository references>`
- **Active register:** `<repository path>`

## Purpose

`<Source-backed outcome. Do not restate unsupported project direction.>`

## Allowed Paths

- `<exact repository path or glob>`

No path not listed here may be changed.

## Forbidden Scope

`<Explicitly list implementation, configuration, project-domain, external-control, later-phase, or other excluded work.>`

## Required Deliverable

`<Concrete artifact or allowed external outcome.>`

## Acceptance Criteria

- `<measurable result>`
- `<measurable result>`

## Required Validation

- `<source and dependency checks>`
- `<allowed-path comparison>`
- `<artifact or behavior validation>`
- `<explicit not-applicable validation where appropriate>`

## Stop Condition

Open one reviewable PR and stop. Do not approve, merge, enable auto-merge, or claim completion before exact merged evidence exists.

## Later-Task Boundary

`<State exactly which later tasks, phases, project work, and external controls this task cannot select, define, configure, or start.>`

## PR Evidence Fields

A task PR must contain:

- `**Task:**` exact task identity;
- `**Phase:**` nonempty active phase or conversion name;
- `**Task definition:**` repository path to this definition;
- `**Active register:**` repository path to the merged active register;
- authority, changed and intentionally unchanged files, validation, limitations, deferred work, internal-review result, boundaries, and human-review boundary.

The generic PR-evidence workflow accepts generic task identities and uses these paths to validate definition and register membership. Direct Project Owner planning tasks may instead state direct authority and their exact allowed-path boundary.
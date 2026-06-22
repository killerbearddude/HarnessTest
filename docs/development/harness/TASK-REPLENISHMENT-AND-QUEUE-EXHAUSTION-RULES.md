# Task Replenishment and Queue Exhaustion Rules

## Purpose

These rules govern the transition from a complete, source-backed task catalog to a small executable horizon. They prevent the harness from treating ad hoc prompts, empty queues, or retired pilot work as authority for new project tasks.

## Definitions

- **Source manifest:** the repository-native record of project source documents, their authority, approval status, and limitations.
- **Roadmap:** the source-backed phase plan derived from the manifest.
- **Full task catalog:** the long-range list of all known source-backed work. It is not execution permission.
- **Executable horizon:** the first three to five complete executable task definitions plus one qualifying gate selected from the approved catalog and governed by a merged active register.
- **Replenishment:** creation of the next bounded executable horizon only from catalog entries whose source authority and dependencies are complete.
- **Retired pilot work:** historical material excluded from current catalog, horizon, and readiness calculations.

## Bootstrap Requirement

A new project may not begin implementation from a generic template until it has approved source documents, a source manifest, a roadmap, a complete task catalog, and a merged register containing the initial executable horizon.

The initial horizon contains only three to five fully executable task definitions and one qualifying gate. The horizon is intentionally smaller than the catalog so the Project Owner can review planning boundaries before task execution begins.

## Replenishment Rule

When an active horizon no longer contains a ready successor after the current task, the harness may replenish it only when:

1. an approved full task catalog exists;
2. the proposed catalog entries have current source-manifest authority;
3. dependencies and decision dependencies are explicit;
4. the selected replenishment output is bounded to three to five complete executable definitions and one qualifying gate;
5. the active register or a direct bounded Project Owner authorization permits the task-authoring work; and
6. no valid harness PR is open.

Replenishment creates planning authority only. It must not execute a task it generates, create implementation by inference, or alter project scope.

## Queue Exhaustion

An empty executable horizon is a controlled stop unless catalog-backed replenishment is explicitly authorized. The harness must report the smallest missing source document, manifest status, roadmap entry, catalog field, decision dependency, task-definition requirement, or Project Owner decision.

A catalog entry is never selected merely because the executable horizon is empty. Retired pilot phases, historical registers, and archived task definitions do not count as ready work or replenishment candidates.

## Active Implementation Phases

An implementation phase is active only when a merged register explicitly authorizes implementation and the required source authority is approved. Governance, planning, documentation, control, repair, and qualifying-gate work are not implementation work solely because they are active.

An implementation phase should retain at least one catalog-backed executable successor beyond the current task when feasible. If the successor horizon cannot be maintained, the harness enters a controlled stop rather than inventing work.

## External Controls

External GitHub settings, rulesets, approvals, bypasses, merge methods, and organization policies are manual Project Owner bootstrap controls unless a separately authorized task explicitly permits observation or administration. They are not normal no-file-change replenishment tasks. The catalog may track the checkpoint and evidence requirement, but must distinguish owner configuration from independently observable repository evidence.

## Pull-Request Boundary

Every planning, replenishment, or task-authoring unit follows the one-task, one-PR boundary. The harness validates source authority, catalog origin, definition completeness, scope, and limitations; opens one reviewable PR; and stops. It never approves, merges, enables auto-merge, or begins generated successor work.

## Current Template Transition

The retired pilot P0–P3 sequence is excluded from this repository's horizon. After the template-conversion register merges, its initial template-conversion horizon is the only selectable work. No project implementation phase is active until a future project completes the bootstrap workflow.
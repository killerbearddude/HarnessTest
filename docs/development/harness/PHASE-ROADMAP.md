# Phase Roadmap

## Purpose

This roadmap is the repository-native authority for identifying future phases that may be considered by `SYS-PLAN-NEXT-TRANCHE`. It does not itself create a phase register, executable task definitions, implementation work, GitHub configuration, workflows, CI, scripts, or product and architecture authority.

A roadmap entry may authorize a bounded planning transition only when it has the required fields in this document and its listed source authority is present and sufficiently specific. A roadmap entry never authorizes the planner to invent behavior or exceed its planning boundary.

## Roadmap States

| State | Meaning | Selection effect |
| --- | --- | --- |
| `ready_for_planning` | The phase purpose, source authority, planning boundary, prohibited scope, and work classification are approved, but its task tranche does not yet exist. | May be considered by `SYS-PLAN-NEXT-TRANCHE` if every trigger condition passes. |
| `planned` | A planning PR for the phase has merged, creating its register, executable task definitions, and qualifying gate definition. | The phase becomes active only as provided by the merged register. |
| `active` | The merged phase register authorizes normal executable-task selection. | Normal ready-task selection applies. |
| `blocked` | Required authority, dependencies, or deterministic phase state are missing, invalid, ambiguous, or conflicting. | No phase work or planning may be selected. |
| `closed` | The phase closed through its designated qualifying gate under the eligibility rules. | No task in the phase may be selected normally. |
| `locked` | The phase lacks an approved purpose, source authority, or Project Owner direction. | Must not be planned or selected. |

`ready_for_planning` differs from `locked`: a ready-for-planning phase has approved bounded purpose and source authority but no tranche yet; a locked phase lacks the approval required to derive a bounded tranche.

## Required Entry Fields

Every roadmap entry that is `ready_for_planning` must identify:

1. phase ID;
2. phase title;
3. bounded purpose;
4. approved source-authority documents;
5. allowed planning boundary;
6. prohibited scope; and
7. work classification: governance, implementation, or mixed.

Exactly one roadmap entry may be `ready_for_planning` for `SYS-PLAN-NEXT-TRANCHE` selection. Multiple entries in that state are an authority conflict and require an explicit Project Owner decision.

## Roadmap Entries

### Phase 3

- **Phase ID:** Phase 3
- **State:** `ready_for_planning`
- **Title:** Implement Repository Enforcement
- **Purpose:** Implement and verify repository-protection and pull-request/CI enforcement required before implementation work may proceed.
- **Work classification:** governance
- **Approved source authority:**
  - `docs/development/harness/REPOSITORY-PROTECTION-REQUIREMENTS.md`
  - `docs/development/harness/PULL-REQUEST-AND-CI-ENFORCEMENT-REQUIREMENTS.md`
  - `HARNESS-CONTROL-BOUNDARY.md`
  - `docs/development/harness/TASK-ELIGIBILITY-AND-COMPLETION-RULES.md`
- **Allowed planning boundary:** Derive only bounded repository-enforcement tasks and one qualifying phase gate.
- **Prohibited scope:** Game implementation, product design, game architecture, graph-domain work, and Phase 4 planning.

## Scope Boundary

This roadmap does not create Phase 3 task registers, executable task definitions, implementation code, GitHub repository settings, branch-protection changes, workflows, CI configuration, scripts, or game work. It does not authorize Phase 4 or later planning.
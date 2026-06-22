# Harness Control Boundary

**Document ID:** HARNESS-TEMPLATE-POLICY-001  
**Status:** Generic template control policy  
**Owner:** Project Owner  
**Scope:** Source-backed task planning, execution, review, retirement, and external-control boundaries

## Purpose

This policy governs a reusable development harness. It converts approved project source documents into bounded repository authority without inventing product direction, architecture, contracts, implementation behavior, or project scope.

The required authority flow is:

```text
approved source documents → source manifest → roadmap → full task catalog
→ executable horizon → one-task PR loop
```

A task catalog is long-range planning, not execution permission. An executable horizon is the small, fully specified subset that may be selected under an active register.

## Core Rules

1. Only one harness work unit may be active and only one valid harness PR may be open at a time.
2. The harness stops after opening a PR.
3. The harness never merges, approves, self-approves, enables auto-merge, bypasses protection, or pushes directly to a protected default branch.
4. Current protected-default-branch and GitHub PR state are authoritative over stale prose.
5. The Project Owner is final approval authority for source documents, external controls, phase retirement, PR review, and phase gates.
6. The harness may execute only an approved executable task in an active authority register, or a direct bounded Project Owner task.
7. The harness may modify only the selected task's exact allowed paths.
8. The harness must report failed, unavailable, owner-attested, and independently observed evidence without conflation.
9. The harness cannot invent project direction, architecture, contracts, product scope, validation commands, implementation behavior, or successor tasks.
10. Every PR must state that no additional task was selected or started.

## Authority Order

When sources conflict, apply this order:

1. Current explicit Project Owner decision.
2. GitHub repository access controls and protected-default-branch state.
3. Approved project source documents and their source-manifest status.
4. Active conversion or project register, roadmap, and full task catalog.
5. Active executable task definition.
6. Repository-native validation and CI evidence.
7. Chat history and summaries.

A conflict at a higher level requires a controlled stop; the harness must not resolve it by inference.

## Project Bootstrap and Task Selection

Before implementation begins in a new project, the project must have:

1. approved source documents;
2. a source manifest that identifies each document's authority and status;
3. a source-backed phase roadmap;
4. a complete task catalog; and
5. a merged active register containing only the first three to five executable definitions and one qualifying gate.

On `Proceed with next task.`, the harness refreshes repository state, checks for an open PR, derives readiness from the active register and exact predecessor evidence, selects the lowest eligible task, performs only that task, opens one PR, and stops. A merged PR never authorizes automatic successor selection.

The executable horizon may be replenished only from approved catalog entries with sufficient source authority. It may not be replenished from ad hoc prompts or inferred work.

## Pilot Retirement and Migration

A direct Project Owner migration decision may retire a non-implementation pilot phase or pilot sequence without marking it completed. Retirement must:

- preserve the affected documents, branches, PRs, and history through an archive or archive map;
- state that retired work is not active authority and may not be selected again;
- identify the successor active authority; and
- state whether any project implementation phase remains active.

Retirement is distinct from task completion and qualifying-gate closure. It does not create implementation authority, unlock later work, or erase pilot history.

After the template-conversion register merges, it is the active authority for this repository. The P0–P3 pilot sequence is historical only; Phase 3 is retired and cannot be resumed, selected, or treated as completed template work. No project implementation phase is active.

## External Controls

Repository settings, rulesets, approvals, bypasses, merge methods, organization policy, and similar external controls are a manual Project Owner bootstrap checkpoint unless a separately authorized task explicitly permits observation or administration. Repository-file and workflow controls are distinct from external administration. The harness must not represent inaccessible external settings as independently verified.

## PR and Reporting Boundary

Before opening a PR, the harness must validate allowed paths, authority, task definition completeness where applicable, dependency evidence, known limitations, and internal review. Every PR must identify the task, objective, authority, changed and intentionally unchanged files, validation outcomes, limitations, deferred work, review result, and human-review requirement.

The harness must stop and report the smallest missing source document, manifest entry, roadmap entry, catalog item, executable definition, external-control attestation, or Project Owner decision when safe execution is not possible.
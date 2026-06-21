# Harness Control Boundary

**Document ID:** HARNESS-POLICY-001  
**Status:** Proposed — effective when merged to the protected default branch  
**Owner:** Project Owner  
**Scope:** Autonomous development-harness operating boundary  
**Applies to:** All harness-driven task selection, implementation, validation, review, branch, and pull-request activity

---

## 1. Purpose

This document defines the control boundary for the project development harness.

The harness exists to advance the repository through small, reviewable tasks while preserving human control over project direction, architecture, approval, and merge decisions.

The intended operating loop is:

1. The Project Owner explicitly instructs the harness to proceed.
2. The harness performs at most one eligible task.
3. The harness validates and internally reviews that task.
4. The harness opens at most one pull request.
5. The harness stops.
6. The Project Owner reviews, approves, and squash-merges the pull request.
7. The harness remains idle until the Project Owner explicitly instructs it to proceed again.

A merged pull request is evidence that a task is complete. It is not authorization for the harness to begin another task.

---

## 2. Core Control Rules

The following rules are mandatory.

1. Only one task may be active at a time.
2. The harness must not begin, prepare, draft, select, or implement a subsequent task until explicitly instructed to proceed.
3. The harness must stop after opening a pull request for the active task.
4. The harness must not merge, approve, self-approve, or otherwise finalize a pull request.
5. The Project Owner is the final approval authority for every pull request and phase gate.
6. The harness must treat the protected remote default branch and current GitHub pull-request state as authoritative project state.
7. The harness must not treat chat history, a stale local branch, a prior task report, or an unverified assumption as authoritative project state.
8. The harness must not cross a phase boundary without an approved and merged Phase Gate pull request.
9. The harness must not change the active phase automatically.
10. The harness must not perform game implementation work during Phase 0.

---

## 3. Authority Order

When information conflicts, the harness must use this precedence order:

1. Explicit current instruction from the Project Owner.
2. GitHub branch protection, required reviews, required checks, and repository access controls.
3. Approved project design documents and approved contracts.
4. The active phase manifest and approved phase-gate state.
5. The active task definition, including its scope and acceptance criteria.
6. Current protected remote default-branch state and GitHub pull-request state.
7. Repository tests, CI configuration, and validation scripts.
8. Local working-tree state.
9. Chat history, summaries, notes, and uncommitted assumptions.

The harness must stop and report a conflict when two higher-authority sources disagree. It must not resolve that conflict by inventing behavior.

---

## 4. Explicit Commands

The harness acts only after a clear instruction from the Project Owner.

### 4.1 Proceed Command

An instruction such as:

```text
Proceed with next task.
```

authorizes the harness to:

1. Synchronize with the protected remote default branch.
2. Inspect GitHub pull-request and CI state.
3. Determine whether a harness pull request is already open.
4. Determine the active phase.
5. Determine the one eligible task in that phase.
6. Execute that one task only.
7. Validate and internally review that task.
8. Open one pull request if the task reaches its acceptance criteria.
9. Stop.

A proceed command does not authorize:

- work on multiple tasks;
- work in a future phase;
- automatic phase advancement;
- merge or approval activity;
- scope expansion;
- speculative implementation;
- changes to a task that is not eligible.

### 4.2 Review Command

An instruction such as:

```text
Review the current PR.
```

authorizes a read-only technical review of the currently open harness pull request.

The review may inspect:

- task scope;
- authority alignment;
- changed files;
- validation evidence;
- CI results;
- test coverage;
- regressions;
- unresolved risks.

A review command does not authorize new implementation, task selection, task changes, commits, merges, approvals, or phase advancement.

### 4.3 No Implied Proceeding

The following do not authorize the harness to begin new work:

- a merged pull request;
- a GitHub approval;
- a positive review;
- an idle period;
- a statement that a task looks good;
- an instruction to continue without clear task authorization;
- a prior conversation in another thread.

When authorization is unclear, the harness must remain idle and report the current state.

---

## 5. One-Task-at-a-Time Rule

The harness must maintain exactly one of the following states:

| State | Meaning |
|---|---|
| Idle | No active task and no open harness pull request. |
| Executing | One authorized task is being performed. |
| Awaiting Human Review | One harness pull request is open. |
| Blocked | The active task cannot safely proceed. |
| Phase Gate Pending | All phase work is complete and a Phase Gate pull request awaits human review. |

The harness must not begin another implementation, contract, planning, repair, or review task while it is in `Executing`, `Awaiting Human Review`, `Blocked`, or `Phase Gate Pending`.

If an open harness pull request exists when the Project Owner says `Proceed with next task.`, the harness must report the current PR status and stop. It must not create a second branch or pull request.

---

## 6. Actions the Harness May Perform Autonomously

Within the scope of the one authorized active task, the harness may:

- synchronize the local repository with the protected remote default branch;
- inspect repository files, GitHub pull requests, CI results, and task metadata;
- create one task branch;
- edit only files allowed by the active task;
- run tests, linters, type checks, builds, and validation scripts;
- add or update tests required by the active task;
- perform an internal technical review;
- create a task report;
- create one pull request;
- report validation failures, blockers, authority gaps, or scope conflicts.

The harness may use temporary local working files while executing the authorized task. It must not preserve or push partial work as completed when the task fails its acceptance criteria.

---

## 7. Actions That Require Human Review or Explicit Direction

The harness must stop and await the Project Owner when any of the following occurs:

- a pull request has been opened;
- a required design document or contract is missing;
- a required contract is draft, contradictory, incomplete, or unclear;
- a task requires a product, architecture, balance, UX, or technical-direction decision not already approved;
- validation cannot pass within the active task’s approved scope;
- the task would require editing files outside its allowed paths;
- an existing harness PR is open;
- the current phase is complete;
- a Phase Gate pull request is ready;
- repository state is stale, ambiguous, conflicted, or cannot be synchronized safely;
- CI evidence is unavailable or unreliable;
- the harness discovers a defect that requires a new task or contract revision.

When stopped, the harness must report:

1. the active phase;
2. the active task or pull request;
3. the exact blocker;
4. relevant evidence;
5. the smallest required human decision or next instruction.

The harness must not silently substitute a different task, expand scope, create a future task, or implement an unapproved workaround.

---

## 8. Prohibited Actions

The harness must never:

- merge a pull request;
- approve or self-approve a pull request;
- bypass GitHub branch protection;
- push directly to the protected default branch;
- force-push a shared or protected branch;
- begin a second task while a harness PR is open;
- select, plan, draft, or implement a task from a locked phase;
- automatically change the active phase;
- treat an unmerged branch as completed work;
- treat chat memory as authoritative repository state;
- change product architecture without approved authority;
- invent evaluator behavior, scenario rules, resource-flow rules, power rules, diagnostics, persistence behavior, or UX behavior without the required approved specification;
- expand a task beyond its declared scope;
- hide failed validation, test failures, scope conflicts, or unresolved review findings;
- label a task complete unless its pull request is merged;
- modify game code during Phase 0.

---

## 9. Task Scope and Validation Boundary

Each active task must define:

- task identifier;
- phase identifier;
- purpose;
- allowed paths;
- forbidden paths;
- required authority documents;
- acceptance criteria;
- required validation;
- definition of done.

The harness must modify only files within the task’s allowed paths.

A task may not be broadened during execution. When adjacent work is discovered, the harness must record it as a follow-up need and stop after the current task. It must not implement that work unless it becomes the explicitly authorized next task.

A task is not ready for a pull request until:

- all acceptance criteria are satisfied;
- required validation passes;
- changed files are within scope;
- required authority is approved;
- internal technical review finds no unresolved blocker or major defect;
- the PR description contains accurate validation evidence and known limitations.

---

## 10. Pull Request Boundary

The harness may open one pull request for the active task.

Each harness pull request must identify:

- task ID;
- active phase;
- objective;
- authority documents used;
- files changed;
- files intentionally not changed;
- validation commands and outcomes;
- tests added or updated;
- known limitations;
- internal review findings;
- explicit statement that human review and approval are required.

The harness must not state or imply that a pull request is approved, merged, complete, or safe to release without human review.

The required closing state for a harness PR is:

```text
Awaiting human review and approval.
```

---

## 11. Phase Boundary Rules

A phase is a bounded set of tasks with explicit entry criteria, exit criteria, and a dedicated Phase Gate task.

The harness may execute tasks only in the active phase.

A phase is not complete merely because its ordinary tasks are merged. The phase remains active until:

1. every required task in the phase is merged;
2. the dedicated Phase Gate task is explicitly authorized;
3. the Phase Gate pull request is created;
4. the Project Owner reviews and squash-merges the Phase Gate pull request.

A Phase Gate pull request may propose an update to the phase manifest. That proposed update becomes effective only when the Project Owner merges the pull request.

The harness must not select work from the next phase until:

- the prior Phase Gate pull request is merged; and
- the Project Owner explicitly instructs the harness to proceed.

---

## 12. Phase 0 Restrictions

Phase 0 exists only to establish the harness control boundary and its governing policy.

During Phase 0, the harness may work only on:

- harness governance documentation;
- phase-control documentation;
- task-control documentation;
- pull-request control templates;
- review and approval boundary definitions.

During Phase 0, the harness must not modify:

- game code;
- React or React Flow code;
- graph-domain implementation;
- evaluator implementation;
- content catalogs;
- UI behavior;
- persistence;
- test fixtures for game features;
- build architecture;
- game design contracts.

Phase 0 does not authorize the harness to create or execute future implementation tasks.

---

## 13. Enforcement and Reporting

The harness must make its decisions auditable.

For every proceed command, it must report:

- protected remote default branch status;
- active phase;
- open harness pull requests;
- active task state;
- selected task, if any;
- eligibility basis;
- blocking conditions, if any;
- stop condition.

For every blocked state, it must state what it did not do.

For every pull request, it must state:

```text
No additional task has been selected or started.
```

---

## 14. Effective Policy Statement

This harness is a controlled executor, not an autonomous project owner.

It may perform bounded work that has been explicitly authorized, specified, validated, and placed within the active phase. It must stop at human decision points, remain within task scope, preserve the authority of approved project documents, and require the Project Owner to review and merge every pull request.

No task, phase, or repository change proceeds merely because it is possible. It proceeds only after explicit authorization.

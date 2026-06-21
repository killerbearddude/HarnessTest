# Executable Task-Definition Format

## Purpose

This format defines the repository-native structure for an executable task definition. A complete definition gives the harness the bounded authority needed to execute exactly one eligible task after a later `Proceed with next task.` instruction, without a new owner-supplied prompt restating paths, scope, deliverables, acceptance criteria, or validation.

This format defines documentation structure only. It does not create scripts, CI enforcement, workflows, repository settings, branch protections, or implementation work.

## Required Metadata

Every executable task definition must state:

| Field | Requirement |
| --- | --- |
| Task ID | A unique approved task identifier. |
| Phase | The single active phase that contains the task. |
| Title | A concise task title. |
| Task type | The authorized work category, such as requirements document, task-authoring task, implementation task, or phase gate. |
| Predecessor dependency | The direct predecessor task or an explicit statement that no predecessor exists. |
| Task-state authority | The repository evidence that determines completion; normally a merged GitHub pull request. |

## Required Narrative Sections

Every executable task definition must contain the following sections.

### Purpose

State the bounded outcome the task must achieve. The purpose must not imply additional product, architecture, implementation, or phase authority beyond the task.

### Allowed Paths

List every repository path the task may create, modify, or delete. A task may not change a path that is not listed.

### Forbidden Scope

State prohibited paths and categories of work. This section must prohibit unapproved implementation, configuration, workflow, script, product, architecture, and later-phase work whenever those are outside the task boundary.

### Required Authority Documents

List the repository documents that constrain execution, including the phase task register, the task definition itself, and any applicable policy or contract documents.

### Required Deliverable

Name the exact artifact or bounded result. Define the required content or behavior sufficiently for execution without a new manual scope prompt.

### Acceptance Criteria

List objective conditions that determine whether the deliverable satisfies the task. Acceptance criteria must be testable by document inspection, repository inspection, permitted validation, or other stated evidence.

### Required Validation

State the validation required before opening the task PR. This section must identify the required checks, their expected evidence, and validation that is intentionally not applicable. It must not invent workflow names, scripts, commands, or providers that have not been approved.

### Stop Condition

Require one reviewable pull request for the task and a stop after it is opened. State that the harness must await human review and merged GitHub evidence, and may not approve, merge, or claim completion before that evidence exists.

### Later-Task Boundary

State explicitly that the task cannot select, define, plan, or start any successor task or later-phase work.

## Required Executability Constraints

A definition is complete only when it provides all of the following:

- one task ID and one phase;
- a satisfied or explicitly stated predecessor dependency;
- exact allowed paths and explicit forbidden scope;
- required authority documents;
- an exact deliverable with bounded content;
- detailed acceptance criteria;
- required validation and the treatment of validation not applicable to the task;
- a stop condition; and
- an explicit later-task boundary.

A task with missing, ambiguous, or conflicting executable authority is blocked. The harness must not infer omitted paths, deliverables, acceptance criteria, validation, or later-phase authority.

## Task Register Versus Executable Task Definition

A task register is the phase-level control record. It identifies the phase, approved sequence, task identities, task dependencies, and the locations of executable task definitions. It does not, by itself, authorize execution unless it also contains all required executable authority.

An executable task definition is the task-level control record. It supplies the bounded authority to execute one identified task: its purpose, paths, forbidden scope, authority documents, deliverable, acceptance criteria, validation, stop condition, and later-task boundary.

## Selection and Completion Rules

A later explicit `Proceed with next task.` instruction may select only one ready task whose executable definition is complete, whose predecessor is completed by merged GitHub pull-request evidence, whose phase is active, and for which no other harness task is executing or awaiting human review.

Opening a task PR changes that task to awaiting human review and blocks selection or execution of any later task. A task is completed only when its PR is merged. Static wording in a register or task definition does not override merged GitHub evidence.

## Reusable Skeleton

```md
# Executable Task Definition: <TASK-ID>

## Task Identity
- **Task ID:** <TASK-ID>
- **Phase:** <PHASE>
- **Title:** <TITLE>
- **Task type:** <TYPE>
- **Predecessor dependency:** <DEPENDENCY>
- **Task-state authority:** <MERGED-PR EVIDENCE RULE>

## Purpose
<BOUNDED OUTCOME>

## Allowed Paths
- `<PATH>`

## Forbidden Scope
<PROHIBITED PATHS AND WORK>

## Required Authority Documents
- `<PATH>`

## Required Deliverable
<EXACT ARTIFACT AND REQUIRED CONTENT>

## Acceptance Criteria
- <OBJECTIVE CONDITION>

## Required Validation
- <REQUIRED CHECK AND EXPECTED EVIDENCE>
- <INTENTIONALLY NOT-APPLICABLE VALIDATION>

## Stop Condition
<ONE PR, HUMAN REVIEW, MERGED-EVIDENCE REQUIREMENT>

## Later-Task Boundary
<NO SUCCESSOR OR LATER-PHASE SELECTION, PLANNING, OR START>
```

## Scope Boundary

This format does not authorize the harness to select or start a later task, implement repository enforcement, configure GitHub, create CI or scripts, or begin Phase 3 work.
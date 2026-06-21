# Pull Request and CI Enforcement Requirements

## Purpose and Status

This document defines the pull-request content, pull-request validation evidence, and future CI enforcement requirements that must be satisfied before the harness may perform implementation work.

These are requirements only. This document does not create, configure, test, verify, or claim active enforcement through GitHub settings, branch protections, workflows, CI, scripts, pull-request templates, or repository automation.

## Pull-Request Identity

Every harness pull request must:

- identify exactly one task ID and one active phase;
- state its objective, allowed scope, and authority documents;
- identify files changed and files intentionally not changed; and
- correspond to one task unless a later approved policy explicitly permits otherwise.

## Required Pull-Request Evidence

Every harness pull request must identify:

- validation commands run and their outcomes;
- tests added, changed, or intentionally not applicable;
- known limitations, deferred work, assumptions, and unresolved risks; and
- whether internal review found blockers, major findings, minor findings, or no findings.

## Human-Review Boundary

Every harness pull request must state that human review and approval are required.

- The harness must stop after opening a pull request.
- The harness must not claim approval, merge readiness, release readiness, or completion before human review and merge.
- The pull request must state that no later task was selected or started.

## Future CI Enforcement Categories

Future CI must validate:

- pull-request metadata and task identity;
- that changes remain within allowed task scope;
- task dependencies and active-phase eligibility;
- required authority-document status;
- repository-appropriate quality checks, including formatting, linting, type checking, build checks, tests, or documentation validation when such checks exist; and
- required evidence and required validation outcomes.

Future CI must fail when required evidence is missing or required validation fails.

## Task and Phase Enforcement

A future enforcement mechanism must reject:

- a pull request that references a task outside the active phase;
- a task with unmet dependencies;
- a pull request when another harness task pull request is already open, unless a later approved policy permits concurrent work; and
- phase-gate closure before all required phase tasks are merged.

## Validation Result Policy

- Failed required validation blocks a pull request from being treated as ready for human review.
- Unavailable validation must be reported explicitly and treated as a blocker unless an approved exception exists.
- Required validation must be distinguished from optional informational checks.

## Implementation Deferral

- This document defines requirements only.
- Workflow names, script names, CI providers, exact commands, check names, and implementation details are deferred to a later explicitly authorized task.
- This document does not claim CI or pull-request enforcement is already active.

## Relationship to Repository Protection

This document complements `REPOSITORY-PROTECTION-REQUIREMENTS.md`.

- Repository protection governs merge and branch controls.
- This document governs pull-request evidence and future automated validation requirements.
- Neither document authorizes implementation of GitHub settings or CI workflows.

## Scope Boundary

This document does not authorize game code, GitHub repository settings, branch-protection changes, workflows, CI configuration, harness scripts, pull-request templates, product authority, Phase 2 or later task definitions, or later-phase work.

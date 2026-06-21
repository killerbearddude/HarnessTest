# Repository Protection Requirements

## Purpose and Status

This document defines the repository-protection requirements that must be satisfied before the harness may perform implementation work.

These are requirements only. This document does not apply, configure, test, verify, or claim enforcement of any GitHub repository setting, branch protection, workflow, CI check, merge queue, or automation.

## Protected Default Branch

- `main` is the protected default branch.
- After repository bootstrap, direct pushes to `main` are prohibited.
- Changes intended for `main` must follow the pull-request requirements in this document.

## Pull-Request Requirement

- All changes to `main` require a pull request.
- Pull requests must be reviewable before merge.
- The harness may open a pull request but may not merge or approve one.

## Human Approval

- At least one human approval is required before merge.
- The harness may not approve or self-approve its own pull request.
- Approvals must be dismissed when new commits are pushed, so merge approval reflects the current pull-request content.

## Required Checks

- Required CI checks must pass before merge.
- The required checks must be identified by the later pull-request and CI-enforcement task.
- This document does not define workflow names, workflow files, test commands, scripts, or other implementation details.

## Branch Freshness

- Before merge, a pull request must be current with `main`.
- An approved equivalent merge-queue or update policy may satisfy this requirement.
- The final enforcement mechanism is deferred to a later task.

## Review Completion

- Required review conversations must be resolved before merge.
- After opening a pull request, the harness must stop and await human review.

## Merge Policy

- Squash merge is the required merge method unless changed by a later explicit Project Owner decision.
- Merge commits and rebase merges are not part of the Phase 1 baseline.

## Administrative Control

- Branch-protection bypass permissions must not be granted to the harness.
- The Project Owner retains final repository-control authority.

## Evidence and Verification

- A later execution task must verify that configured controls match these requirements.
- This document does not claim that any required control is already configured or active.

## Exceptions

- The initial repository bootstrap commit was a one-time exception because no pull-request base existed.
- No further exception is implied.
- Any future exception requires an explicit Project Owner decision recorded in a reviewable pull request.

## Scope Boundary

This document does not authorize changes to GitHub repository settings, branch protections, GitHub workflows, CI configuration, harness scripts, game code, product authority, or later-phase work.

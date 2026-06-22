# External Control Checklist

## Purpose

External GitHub and organization controls are manual Project Owner bootstrap checkpoints. They are not ordinary no-file-change harness tasks and must not be represented as automatically configured by repository files or workflows.

## Evidence Classes

| class | meaning |
| --- | --- |
| Owner-configured setting | The Project Owner manually configured the external setting. Record attestation, date, and scope. |
| Independently observable repository evidence | The connected toolset can directly observe repository metadata, PR evidence, workflow evidence, or other stated evidence. |
| Unavailable for connected-tool inspection | The required setting cannot be inspected through the currently connected toolset. Do not claim independent verification. |
| Repository-file or workflow control | A tracked repository artifact can enforce or document part of the control; it does not prove external administration. |

## Manual Project Owner Checkpoint

Before project implementation begins, the Project Owner must decide and record applicable external controls, including:

- default-branch protection or rulesets;
- direct-push and bypass policy;
- required human approvals and stale-review behavior;
- required checks and branch-freshness policy;
- review-conversation resolution;
- merge methods and merge queue behavior;
- organization policy, access, and retention controls; and
- any project-specific external services or compliance controls.

## Evidence Table

Use this table in a future project control record:

| required control | owner configuration evidence | independently observable repository evidence | connected-tool inspection status | repository-file or workflow control | limitation or decision |
| --- | --- | --- | --- | --- | --- |

## Boundary Rules

- Do not claim a setting is independently verified unless direct evidence is available.
- Do not represent owner configuration as a harness action.
- Do not use an empty branch or a no-file-change task merely to evidence external administration.
- A repository workflow may validate repository-native evidence, but cannot substitute for inaccessible external controls.
- Missing external-control authority creates a controlled stop or a Project Owner decision request, not inferred configuration.
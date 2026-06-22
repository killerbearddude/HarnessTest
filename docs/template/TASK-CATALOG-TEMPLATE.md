# Task Catalog Template

## Purpose

The full task catalog is the long-range, source-backed plan derived from the roadmap. It provides traceability and sequencing. It is not permission to execute tasks.

## Required Catalog Fields

Every catalog row must contain:

| field | requirement |
| --- | --- |
| task ID | stable generic task identity |
| phase | roadmap phase reference |
| title | concise task name |
| purpose | source-backed intended outcome |
| task type | planning, control, implementation, verification, gate, repair, or owner-defined type |
| predecessor or dependency | exact task, decision, or source dependency |
| source-authority documents | source-manifest IDs and repository references |
| expected deliverable | concrete artifact or externally observable outcome |
| primary acceptance outcome | measurable completion result |
| decision dependency, if any | required owner decision or `none` |
| catalog status | proposed, source-backed, planned, in-horizon, active, completed, blocked, retired, or equivalent approved state |
| executable horizon | `yes` or `no` |

## Catalog Rules

- Every entry must trace to approved source authority.
- A catalog entry with missing decision or source authority remains blocked.
- Only entries marked `in-horizon` and represented by a complete definition in a merged active register may be selected.
- A completed entry remains catalog history; a retired entry is not treated as completed unless exact merged task evidence exists.
- The catalog may be larger than the executable horizon. The horizon remains limited to three to five complete definitions plus one qualifying gate.

## Catalog Row Skeleton

| task ID | phase | title | purpose | task type | predecessor or dependency | source-authority documents | expected deliverable | primary acceptance outcome | decision dependency, if any | catalog status | executable horizon |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `<PROGRAM>-T01` | `<PHASE>` | `<title>` | `<purpose>` | `<type>` | `<dependency>` | `<manifest IDs>` | `<deliverable>` | `<acceptance>` | `<decision or none>` | `source-backed` | `no` |
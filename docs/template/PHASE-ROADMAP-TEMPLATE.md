# Phase Roadmap Template

## Purpose

The roadmap is the source-backed phase plan between the source manifest and the full task catalog. It describes bounded planning; it is not permission to execute a phase task.

## Required Phase Entry Fields

| field | requirement |
| --- | --- |
| phase ID | stable phase identifier |
| title | concise phase name |
| purpose | outcome supported by source authority |
| source-authority documents | source-manifest IDs and repository references |
| planning boundary | what may be derived during planning |
| prohibited scope | work excluded from the phase |
| phase type | planning, governance, implementation, control, gate, or owner-defined type |
| decision dependency | required decision, if any |
| roadmap status | state from the controlled status set |
| catalog reference | related full task catalog entries |

## Controlled Status Set

| status | meaning |
| --- | --- |
| proposed | not yet source-backed; not selectable |
| source-backed | source authority exists; catalog planning may be authorized |
| planned | catalog and horizon artifacts are being reviewed; not executable |
| active | merged register authorizes an executable horizon |
| blocked | a required source, decision, dependency, or control is missing |
| closed | qualifying gate closure evidence exists |
| retired | preserved history; not completed by retirement and not selectable |

## Roadmap Rules

- A roadmap entry must cite source-manifest authority before it can produce catalog entries.
- A roadmap entry does not create executable definitions, implementation authority, or a task selection by itself.
- Only a merged active register may expose catalog entries as an executable horizon.
- A direct Project Owner retirement decision may mark a non-implementation pilot phase retired without marking it closed; the decision must preserve history and identify successor authority.
- A new phase or scope not supported by approved sources remains blocked.

## Generic Example Structure

```text
Phase: <PROGRAM>-<NN>
Purpose: <source-backed outcome>
Source authority: <manifest IDs>
Planning boundary: <bounded derivation>
Prohibited scope: <excluded work>
Status: source-backed
Catalog reference: <catalog entry IDs>
```
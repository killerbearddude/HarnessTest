# Project Bootstrap

## Required Starting Condition

A new project must first supply approved source documents. The harness cannot begin implementation from a generic template, a conversation prompt, or an assumed product direction.

Source documents may include approved direction, constraints, requirements, policies, contracts, architecture decisions, external-control decisions, or other authoritative materials. Their type and location are project-specific; their authority status must be recorded before planning.

## Required Workflow

1. **Add source documents.** Store the project-provided source documents in repository paths chosen by the Project Owner.
2. **Create a source manifest.** Create a repository-native manifest that records each source document's path, owner, authority level, approval status, scope, and limitation.
3. **Derive a project roadmap.** Create a roadmap from manifest-approved sources. Every phase records purpose, source authority, boundary, prohibited scope, decision dependency, and status.
4. **Derive a full task catalog.** Create the long-range catalog from the roadmap and source manifest. Every catalog entry must use the fields in `TASK-CATALOG-TEMPLATE.md`.
5. **Create the initial executable horizon.** Select only the first three to five catalog-backed tasks that can be fully specified, plus one qualifying gate. Create complete executable definitions using `EXECUTABLE-TASK-DEFINITION-TEMPLATE.md` and place them in an active register.
6. **Begin the normal loop.** Only after the horizon register merges may a later explicit `Proceed with next task.` select the lowest eligible task.
7. **Replenish only from the catalog.** When the horizon needs successors, derive a new bounded horizon only from approved catalog entries and their source authority.

## Source Manifest Minimum Fields

The future project's source manifest must record:

| field | purpose |
| --- | --- |
| source ID | stable reference used by roadmap, catalog, and tasks |
| repository path or external reference | location of the source |
| owner | accountable authority holder |
| authority level | binding, advisory, pending, retired, or equivalent owner-defined state |
| approval status | current decision status |
| scope | what the source authorizes or constrains |
| limitation | what the source does not establish |
| reviewed date | freshness evidence |

## No-Invention Boundary

The harness must not invent product direction, architecture, contracts, scope, acceptance criteria, implementation behavior, or external-control requirements not supported by approved source documents. Missing authority produces a controlled stop and the smallest bounded request for a decision or source update.

## Bootstrap Output Boundary

Bootstrap creates planning and task authority only. It does not automatically create implementation, configure external settings, or select a task it generates. Human review and merge remain required before the normal one-task PR loop starts.
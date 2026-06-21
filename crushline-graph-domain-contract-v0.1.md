# Crushline Graph Domain, Port, and Command Contract v0.1

**Document ID:** CL-GRAPH-001  
**Revision:** 0.1.0  
**Status:** Review Draft  
**Owner:** Crushline Project Owner  
**Recommended repository path:** `docs/contracts/crushline-graph-domain-contract-v0.1.md`  
**Depends on:** *Crushline: Design and Production Systems Baseline v1.0*  
**Required before:** Persistent graph state, port templates, graph commands, import validation, durable save implementation, or React Flow projection synchronization  
**Next review trigger:** Before implementation begins for persistent graph commands or content-driven port generation

---

## 1. Purpose and Authority

This contract defines the persistent production-graph domain for Crushline. It turns the baseline's graph authority rules into an implementation-ready boundary without defining the production evaluator, scenario balance, player-facing diagnostic copy, save migration policy, or temporal certification simulation.

The contract owns:

- graph identity and canonical ordering;
- persistent node, port, and link entities;
- node kinds and their structural responsibilities;
- port materialization from content templates;
- link lifecycle, cardinality, and structural validity;
- graph command behavior and atomicity;
- graph import validation and malformed-import recovery;
- React Flow projection synchronization.

This contract does **not** own:

- material-flow equations, rates, throughput, or conservation arithmetic;
- power demand, brownout policy, or power margin calculation;
- scenario availability, unlocks, balance, or objective thresholds;
- player-facing diagnostic messages or remediation language;
- persistence packaging, migrations, or cross-version recovery;
- route scoring, route proof, or Closed-Line temporal certification.

### 1.1 Precedence

The approved Design Baseline owns product identity, durable architecture decisions, non-goals, and system authority. This contract may define executable graph-domain detail inside that boundary. It may not override a locked baseline decision.

When there is a conflict, precedence is:

1. Approved Crushline Design and Production Systems Baseline.
2. Approved Graph Domain, Port, and Command Contract.
3. Approved Evaluator and Material-Flow Contract.
4. Approved Power Ledger and Infrastructure Contract.
5. Approved Scenario and Content Contract.
6. Approved Diagnostic UX, Persistence, Route-Proof, and visual-design contracts.
7. Implementation notes, prototypes, and exploratory drafts.

No UI convenience, prototype behavior, or implementation note may override an approved contract.

### 1.2 Companion-contract dependencies

This contract must be approved before the following work begins:

| Work item | Required authority |
|---|---|
| Persistent `ProductionGraph` state | This contract |
| Node/port/link creation and deletion | This contract |
| Content-driven port generation | This contract + Scenario and Content Contract |
| React Flow synchronization | This contract |
| Material flow and production evaluation | This contract + Evaluator Contract |
| Power behavior | This contract + Power Contract |
| Save packaging and migration | This contract + Persistence Contract |
| Player-facing structural errors | This contract + Diagnostic UX Contract |

---

## 2. Scope and Non-Goals

### 2.1 In scope

This version supports a single-player, local, persistent directed graph containing sources, machines, sinks, objective sinks, and generators/infrastructure nodes.

It supports:

- finite 2D node positions;
- materialized input and output ports;
- one directed link per output and one directed link per input;
- content-derived port templates;
- machine recipe selection and port reconciliation;
- deterministic commands and structural validation;
- cycles as representable graph structures;
- graph/UI projection through React Flow.

### 2.2 Explicit non-goals

This version does not support:

- collaborative editing or concurrent command conflict resolution;
- undo/redo, command history, transactions, or macro commands;
- manual user-authored ports;
- manually selected resource identity on a link;
- graph-routed electrical power;
- splitters, mergers, buses, buffers, storage, priority routing, or automation nodes;
- two-way ports, bottom ports, top ports, or arbitrary port placement;
- nested graphs, groups, subgraphs, or graph templates;
- evaluator decisions about wrong-resource outcomes;
- save migration algorithms;
- player-facing diagnostic text.

A future system requiring one of these capabilities must add or revise an approved contract before implementation.

---

## 3. Durable Graph Invariants

The following invariants are binding.

1. `ProductionGraph` is the authoritative graph state. React Flow is a projection and interaction adapter.
2. Links connect ports only. A link never stores a freely selected material or rate.
3. Sources and recipe output streams determine produced materials. The evaluator determines actual flow.
4. Recipe output stream role, not global resource identity, classifies output as primary, byproduct, waste, recovered, or catalyst return.
5. Every persisted port belongs to exactly one persisted node.
6. Every persisted link references exactly one existing output port and one existing input port.
7. Structural graph validity is independent from economic usefulness. A graph may be structurally valid and still fail simulation or objectives.
8. Graph commands are atomic. A rejected command changes no persistent graph entity.
9. All externally visible command results and validation reports have deterministic ordering.
10. The graph domain does not create, consume, or simulate material quantities.
11. Cycles are allowed structurally. The evaluator later decides whether a scenario can evaluate them.
12. A disabled node remains structurally present. Disabled state is not a reason to delete links or reject otherwise valid graph connections.

### 3.1 Conservation-safe boundary

For Crushline, **conservation-safe** means the evaluator may not silently create or destroy represented stream quantities outside explicitly authored recipe conversion, disposal, loss, leakage, recovery, or other approved stream rules. It does not require real-world stoichiometric chemistry. This contract preserves the structural authority needed for that future evaluator rule; it does not itself calculate flow.

---

## 4. Identity, Canonical Ordering, and Graph Snapshot

### 4.1 Entity IDs

The graph uses opaque string identifiers.

```ts
export type GraphId = string;
export type NodeId = string;
export type PortId = string;
export type LinkId = string;
```

An entity ID must:

- be non-empty;
- be unique within its entity type in one graph;
- remain stable while the entity exists;
- never be reassigned to a different entity in the same graph history;
- be treated as opaque by UI and evaluator code.

The implementation may use UUID-like IDs, monotonic IDs, or another collision-resistant generator. Tests must be able to inject deterministic IDs.

### 4.2 ID factory requirement

Creation commands use a `GraphIdFactory` supplied by the graph-domain implementation.

```ts
export interface GraphIdFactory {
  createGraphId(): GraphId;
  createNodeId(graph: ProductionGraph): NodeId;
  createPortId(graph: ProductionGraph): PortId;
  createLinkId(graph: ProductionGraph): LinkId;
}
```

If the factory cannot produce a unique valid ID, the command is rejected without mutation.

### 4.3 Canonical collection order

`nodes`, `ports`, and `links` are canonical arrays.

- Creation appends an entity to its relevant array.
- Commands do not reorder surviving entities.
- Import preserves valid incoming array order after validation.
- Removal preserves the relative order of all surviving entities.
- Any result list uses canonical array order unless a section explicitly states otherwise.

This ordering is used for deterministic command summaries, import normalization, UI projection, and future evaluator tie-breaking.

### 4.4 Graph snapshot

```ts
export interface ProductionGraph {
  schemaVersion: 1;
  graphId: GraphId;
  revision: number;
  nodes: ProductionNode[];
  ports: ProductionPort[];
  links: ProductionLink[];
}
```

Rules:

- `revision` begins at `0` for a newly created graph.
- Every applied graph command increments `revision` by exactly `1`.
- Rejected commands do not change `revision`.
- Imported graphs retain their serialized revision after validation.
- `schemaVersion` must be exactly `1` for this contract version.

---

## 5. Node Domain Model

### 5.1 Node kinds

```ts
export type NodeKind =
  | "source"
  | "machine"
  | "sink"
  | "objective_sink"
  | "generator";
```

| Node kind | Structural role | Domain meaning owned elsewhere |
|---|---|---|
| `source` | Materializes output ports from a source definition. | Availability, source capacity, depletion, and produced material. |
| `machine` | Materializes base and recipe ports from a machine and selected recipe. | Transformation, rates, byproducts, and operating behavior. |
| `sink` | Materializes input ports from a sink definition. | Disposal, treatment, storage, or handling acceptance. |
| `objective_sink` | Materializes input ports used as delivery boundaries. | Objective measurement and completion. |
| `generator` | Materializes non-power material input/output ports from a generator definition. | Global power contribution and fuel/operating behavior. |

No node kind creates a generic routed power output in this version. The baseline global power ledger is not represented through power links.

### 5.2 Common node fields

```ts
export interface NodePosition {
  x: number;
  y: number;
}

export interface NodeBase {
  id: NodeId;
  kind: NodeKind;
  definitionKey: string;
  position: NodePosition;
  enabled: boolean;
}
```

Position rules:

- `x` and `y` must be finite JavaScript numbers.
- The graph domain does not impose canvas bounds.
- Position is persistent graph layout state.
- Viewport, zoom, hover, and selection are UI state, not node fields.

### 5.3 Node variants

```ts
export interface SourceNode extends NodeBase {
  kind: "source";
}

export interface MachineNode extends NodeBase {
  kind: "machine";
  recipeKey: string | null;
}

export interface SinkNode extends NodeBase {
  kind: "sink";
}

export interface ObjectiveSinkNode extends NodeBase {
  kind: "objective_sink";
}

export interface GeneratorNode extends NodeBase {
  kind: "generator";
}

export type ProductionNode =
  | SourceNode
  | MachineNode
  | SinkNode
  | ObjectiveSinkNode
  | GeneratorNode;
```

`definitionKey` identifies a definition owned by the active catalog/scenario context. It must not be changed by a generic graph command in v0.1. Replacing a source, machine, sink, objective sink, or generator definition requires delete-and-create or a future dedicated contract extension.

### 5.4 Enabled state

`enabled` is persisted operational state.

- A graph command may toggle node enabled state.
- Enabling or disabling a node does not create, remove, or invalidate ports or links.
- The graph domain does not decide the evaluator consequences of disabled state.
- UI may show disabled nodes and links, but may not silently remove them.

---

## 6. Port Domain Model and Template Authority

### 6.1 Port direction, side, and role

```ts
export type PortDirection = "input" | "output";
export type PortSide = "left" | "right";

export type PortRole =
  | "material_input"
  | "material_output"
  | "byproduct_output"
  | "waste_output"
  | "sink_input"
  | "objective_input"
  | "fuel_input";
```

Rules:

- Inputs render on the left; outputs render on the right.
- `PortSide` is presentation metadata constrained by direction in v0.1.
- Bottom, top, arbitrary side placement, and two-way ports are not supported.
- `PortRole` describes a structural/presentation category. It does not declare a material identity, rate, or evaluator result.

### 6.2 Port template

A catalog resolves the active port layout for a node.

```ts
export interface PortTemplate {
  templateKey: string;
  label: string;
  role: PortRole;
  direction: PortDirection;
  side: PortSide;
  displayOrder: number;
  streamBindingKey: string | null;
}
```

`templateKey` is a stable semantic key within a resolved node layout. It must not be reused for a different role, direction, side, or stream binding. A content change that changes that meaning must introduce a new template key.

`streamBindingKey` identifies the recipe, source, sink, or objective stream slot that this port represents. The Graph Domain contract does not interpret stream quantities or materials; it preserves the binding for content/evaluator resolution.

### 6.3 Persisted port instance

```ts
export interface ProductionPort {
  id: PortId;
  nodeId: NodeId;
  templateKey: string;
  role: PortRole;
  direction: PortDirection;
  side: PortSide;
  displayOrder: number;
  streamBindingKey: string | null;
}
```

Authority split:

| Concern | Authority |
|---|---|
| Stable port ID and node ownership | `ProductionPort` |
| Current structural direction, role, side, display order, stream binding | Resolved `PortTemplate`, copied into the materialized port and validated against it |
| Material identity, rate, input acceptance, output behavior | Scenario/Content and Evaluator contracts |
| React Flow handle rendering | Graph UI adapter projection |

Ports are persisted because links require stable endpoint identity. Ports are not independently user-authored. Their shape derives from the node's resolved template layout.

### 6.4 Port materialization

A node's ports are materialized only by:

1. creating a node; or
2. changing a machine's selected recipe.

There is no public `add_port` or `remove_port` command in v0.1.

The resolver must return a complete, deterministic list of templates for the requested node state:

```ts
export interface GraphCatalogResolver {
  resolveNodeDefinition(
    kind: NodeKind,
    definitionKey: string,
  ): { found: true } | { found: false; reason: string };

  resolvePortTemplates(
    node: ProductionNode,
  ): ReadonlyArray<PortTemplate> | null;

  canSelectRecipe(
    node: MachineNode,
    recipeKey: string | null,
  ): { allowed: true } | { allowed: false; reason: string };
}
```

The exact catalog schema belongs to the Scenario and Content Contract. The resolver is the Graph Domain boundary to that schema.

### 6.5 Recipe change and port reconciliation

Only a `machine` node may change `recipeKey`.

When a recipe changes:

1. Validate that the machine and selected recipe are allowed by the resolver.
2. Resolve the new template list before modifying graph state.
3. Match existing ports to new templates by `templateKey`.
4. Preserve a matched port ID only when the template's `role`, `direction`, `side`, and `streamBindingKey` are unchanged.
5. Create a new port for every unmatched new template.
6. Remove every unmatched old port.
7. Remove every link incident to a removed port.
8. Retain links on preserved ports when they remain structurally valid.
9. Apply the node recipe change, port reconciliation, and cascading link deletion atomically.

A recipe change may create a graph that is economically poor or operationally invalid. The Graph Domain contract does not remove a retained link merely because its new recipe stream meaning is unfavorable. That is evaluator territory.

A machine with `recipeKey: null` resolves only the machine definition's base-port templates. If no base ports exist, it resolves no ports.

---

## 7. Link Domain Model and Structural Cardinality

### 7.1 Link structure

```ts
export interface ProductionLink {
  id: LinkId;
  fromPortId: PortId;
  toPortId: PortId;
}
```

A link carries no material key, rate, power value, route label, or user-selected override.

### 7.2 Cardinality

v0.1 supports only one-to-one directed links:

| Port direction | Maximum incoming links | Maximum outgoing links |
|---|---:|---:|
| `input` | 1 | 0 |
| `output` | 0 | 1 |

There is no implicit splitting, merging, bus behavior, storage, or routing priority.

A future splitter, merger, buffer, or automation system must be introduced as an explicit node/domain extension with its own approved port/cardinality rules.

### 7.3 Link creation rules

A `create_link` command is accepted only when all conditions are true:

1. Both ports exist.
2. `fromPortId` and `toPortId` are different.
3. The ports belong to different nodes.
4. The source port has direction `output`.
5. The target port has direction `input`.
6. No exact duplicate link exists.
7. The source output has no existing outgoing link.
8. The target input has no existing incoming link.

The command does not inspect resource compatibility, rates, recipe semantics, power, waste, objective relevance, or node enabled state.

### 7.4 Replacement policy

No connection is implicitly replaced.

When cardinality is full, `create_link` is rejected with `cardinality_exceeded`. The caller must explicitly delete the old link before creating a replacement. This rule prevents accidental graph data loss during drag-to-connect interaction.

### 7.5 Cycles

The graph domain allows directed cycles. It does not detect, block, or solve them as part of structural validation.

The Evaluator Contract owns cycle diagnostics and scenario evaluation policy.

---

## 8. Graph Commands and Atomic Mutation

### 8.1 Command set

v0.1 defines the following graph commands:

```ts
export type GraphCommand =
  | CreateNodeCommand
  | DeleteNodeCommand
  | MoveNodesCommand
  | SetNodeEnabledCommand
  | SetMachineRecipeCommand
  | CreateLinkCommand
  | DeleteLinkCommand;
```

No other persistent graph mutation is allowed without a contract revision.

### 8.2 Command shapes

```ts
export interface CreateNodeCommand {
  kind: "create_node";
  nodeKind: NodeKind;
  definitionKey: string;
  position: NodePosition;
  recipeKey?: string | null;
}

export interface DeleteNodeCommand {
  kind: "delete_node";
  nodeId: NodeId;
}

export interface MoveNodesCommand {
  kind: "move_nodes";
  moves: ReadonlyArray<{ nodeId: NodeId; position: NodePosition }>;
}

export interface SetNodeEnabledCommand {
  kind: "set_node_enabled";
  nodeId: NodeId;
  enabled: boolean;
}

export interface SetMachineRecipeCommand {
  kind: "set_machine_recipe";
  nodeId: NodeId;
  recipeKey: string | null;
}

export interface CreateLinkCommand {
  kind: "create_link";
  fromPortId: PortId;
  toPortId: PortId;
}

export interface DeleteLinkCommand {
  kind: "delete_link";
  linkId: LinkId;
}
```

### 8.3 Command result

```ts
export type GraphCommandCode =
  | "applied"
  | "invalid_argument"
  | "not_found"
  | "duplicate_id"
  | "invalid_position"
  | "invalid_node_kind"
  | "invalid_definition"
  | "invalid_recipe"
  | "invalid_port_template"
  | "invalid_connection"
  | "duplicate_link"
  | "cardinality_exceeded"
  | "id_generation_failed"
  | "catalog_mismatch";

export interface GraphCommandResult {
  applied: boolean;
  code: GraphCommandCode;
  graph: ProductionGraph;
  summary: GraphMutationSummary;
  issues: GraphValidationIssue[];
}
```

On rejection:

- `applied` is `false`;
- `graph` is semantically unchanged from the input graph;
- `revision` is unchanged;
- `summary` contains no changes;
- `issues` contains deterministic structural issue records.

On success:

- `applied` is `true`;
- `graph.revision` increments by exactly `1`;
- `summary` describes the committed mutation;
- `issues` is empty unless a future command explicitly documents non-blocking structural warnings.

### 8.4 Mutation summary

```ts
export interface GraphMutationSummary {
  createdNodeIds: NodeId[];
  updatedNodeIds: NodeId[];
  removedNodeIds: NodeId[];
  createdPortIds: PortId[];
  updatedPortIds: PortId[];
  removedPortIds: PortId[];
  createdLinkIds: LinkId[];
  removedLinkIds: LinkId[];
}
```

Ordering rules:

- Created IDs appear in creation/append order.
- Updated IDs appear in canonical collection order.
- Removed IDs appear in their canonical collection order immediately before the command.
- A cascading deletion reports links before nothing else only in its dedicated arrays; consumers must not infer cross-array timing from summary array order.
- Empty categories are represented by empty arrays.

The summary is domain change metadata. It does not contain UI selection, React Flow viewport, evaluator results, or player-facing messages.

### 8.5 Atomicity

Every command follows this logical sequence:

1. Validate command shape and finite values.
2. Resolve all referenced nodes, ports, definitions, recipes, and templates.
3. Build all new IDs, ports, links, and mutation summary data in temporary structures.
4. Validate the complete post-command graph structure.
5. Commit all persistent changes as one graph revision.
6. Return the new graph and summary.

If any step fails, the command is rejected and no persistent graph entity changes.

### 8.6 Node deletion cascades

Deleting a node atomically removes:

1. the target node;
2. every port owned by that node;
3. every link incident to one of those ports.

No orphaned ports or links may remain.

### 8.7 Recipe-change cascades

Changing a machine recipe may remove ports. Every link incident to a removed port is removed in the same atomic command.

No automatic reconnection is attempted.

### 8.8 Move command behavior

`move_nodes` is atomic across the provided move set.

- Each node ID must exist exactly once in the command.
- Each target position must be finite.
- If any move is invalid, no node moves.
- A move command must contain at least one effective position change.
- If every requested position exactly equals its current position, reject the command with `invalid_argument`; do not increment revision.

---

## 9. Structural Validation

### 9.1 Validation report

```ts
export type GraphValidationSeverity = "error" | "warning";

export type GraphValidationIssueCode =
  | "unsupported_schema_version"
  | "invalid_graph_id"
  | "duplicate_node_id"
  | "duplicate_port_id"
  | "duplicate_link_id"
  | "invalid_position"
  | "invalid_node_kind"
  | "invalid_definition"
  | "invalid_recipe"
  | "orphan_port"
  | "duplicate_port_template"
  | "port_template_mismatch"
  | "invalid_port_direction"
  | "invalid_port_side"
  | "invalid_port_role"
  | "invalid_link_source"
  | "invalid_link_target"
  | "self_port_link"
  | "same_node_link"
  | "duplicate_link"
  | "input_cardinality_exceeded"
  | "output_cardinality_exceeded";

export interface GraphValidationIssue {
  code: GraphValidationIssueCode;
  severity: GraphValidationSeverity;
  entityType: "graph" | "node" | "port" | "link";
  entityId: string | null;
  relatedEntityIds: string[];
  details: Record<string, string | number | boolean | null>;
}
```

These records are machine-readable structural facts. The Diagnostic UX contract maps accepted relevant issues into player-facing language and presentation.

### 9.2 Required structural checks

A fully valid graph must satisfy all of the following:

- supported schema version;
- valid unique graph ID;
- valid unique IDs per node, port, and link collection;
- finite node positions;
- supported node kinds;
- valid catalog definition references;
- valid selected recipe references for machine nodes;
- every port references an existing node;
- every node's materialized ports match its resolved template layout exactly;
- no duplicate `templateKey` exists on a node;
- every link references existing ports;
- every link is output-to-input;
- no self-port links;
- no same-node links;
- no duplicate exact links;
- no input or output exceeds v0.1 cardinality.

### 9.3 Deterministic issue ordering

Validation issues are ordered by:

1. severity (`error` before `warning`);
2. entity collection order: graph, node, port, link;
3. canonical entity array order;
4. issue-code lexical order;
5. related entity canonical order.

This ordering is a testable contract.

---

## 10. Import Validation and Malformed-Import Recovery

### 10.1 Import boundary

The Graph Domain importer accepts only graph documents already selected by the Persistence Contract as candidates for schema v1 graph validation.

The importer does not perform save migration. It validates one supported graph schema against one active catalog/scenario context.

### 10.2 Import process

Import must:

1. parse the candidate data without mutating the active graph;
2. verify the graph schema version;
3. validate primitive field shapes and IDs;
4. resolve all definition and recipe references against the active catalog resolver;
5. validate port-template materialization;
6. validate link structure and cardinality;
7. produce a canonical `ProductionGraph` only if all blocking issues are absent.

### 10.3 Failure behavior

On malformed or incompatible import:

- the active in-memory graph remains unchanged;
- no partial graph is returned as valid;
- the importer returns a deterministic validation report;
- the importer does not silently delete, reconnect, rename, or repair entities;
- the UI may offer recovery/export options, but those belong to the Persistence and Diagnostic UX contracts.

### 10.4 Catalog mismatch

If a graph references a missing definition, recipe, or required port template, the import fails with a catalog mismatch or specific structural validation issue. The graph domain must not invent substitute ports or remap content keys.

Migration, aliasing, deprecated-key replacement, and user recovery belong to the Persistence Contract.

---

## 11. React Flow Projection and Synchronization

### 11.1 Projection rule

React Flow is a projection of `ProductionGraph`.

```text
ProductionGraph -> React Flow nodes/handles/edges -> rendered UI
```

The graph domain must not read React component identity, DOM state, hover state, selection state, or viewport state as persistent graph authority.

### 11.2 Stable mapping

| Domain entity | React Flow projection |
|---|---|
| `ProductionNode.id` | React Flow node `id` |
| `ProductionPort.id` | React Flow handle `id` |
| `ProductionLink.id` | React Flow edge `id` |
| `NodePosition` | React Flow node position |
| `ProductionPort.direction` | Source or target handle behavior |
| `ProductionPort.side` | Handle side placement |

The adapter must not generate substitute graph IDs for React Flow entities.

### 11.3 UI-to-domain command routing

React Flow interactions must become domain commands:

| UI interaction | Required domain command |
|---|---|
| Add a node | `create_node` |
| Delete a node | `delete_node` |
| Complete a connection gesture | `create_link` |
| Delete an edge | `delete_link` |
| Commit node position after drag | `move_nodes` |
| Toggle operational state | `set_node_enabled` |
| Select a machine recipe | `set_machine_recipe` |

The UI must not remove or create persisted graph entities solely through local React Flow state changes.

### 11.4 Transient interaction state

During a drag or connection gesture, the UI may hold transient local state for responsiveness.

On gesture commit:

- the UI emits one domain command;
- on command success, it renders the new projection;
- on command rejection, it restores the authoritative projection and displays applicable diagnostics through the Diagnostic UX system.

Selection, hover, panel visibility, viewport, and temporary connection previews are UI state. They are not part of `ProductionGraph`.

### 11.5 Synchronization rule

The application processes graph commands serially in local order. A command result is the sole authority for the next persistent graph revision. This v0.1 contract does not support concurrent multiplayer edits or merging independent command streams.

---

## 12. Boundary to Evaluator, Power, Content, Diagnostics, and Persistence

### 12.1 Evaluator boundary

The future Evaluator Contract receives a structurally valid `ProductionGraph` plus resolved content. It owns:

- topological ordering and cycle policy;
- stream quantities, rates, capacity, and run fractions;
- source and recipe output material identity;
- input consumption and output allocation;
- surplus, handling, recovery, and objective delivery calculations;
- simulation diagnostics.

The Graph Domain contract deliberately does not calculate these outcomes.

### 12.2 Power boundary

The future Power Contract owns:

- generator contribution;
- machine operating and standby demand;
- global power ledger calculation;
- power margin;
- brownout behavior;
- power diagnostics.

This contract only provides generator and machine graph entities plus their catalog references.

### 12.3 Scenario and content boundary

The Scenario and Content Contract owns:

- content definitions and keys;
- which node definitions and recipes are available;
- port template source data;
- recipe compatibility;
- source/sink/objective/generator definitions;
- scenario restrictions and progression availability.

### 12.4 Diagnostics boundary

This contract returns stable structural codes and affected entities. The Diagnostic UX Contract owns message text, hierarchy, remediation language, suppression, and player-comprehension testing.

### 12.5 Persistence boundary

This contract validates a graph schema. The Persistence Contract owns:

- save container fields;
- save/catalog/scenario/progression versioning;
- migrations;
- legacy aliases;
- invalid-save recovery flows;
- raw JSON import/export UI.

---

## 13. Required Acceptance Fixtures

Before persistent graph implementation is accepted, tests must cover these fixed graph-domain fixtures. These are not scenario balance fixtures and require no recipe rates.

| Fixture | Required proof |
|---|---|
| Create source | Valid source node creates resolved material output ports in deterministic order. |
| Create machine with recipe | Valid machine creates recipe-derived ports with stable IDs and template bindings. |
| Create machine with no recipe | Machine resolves only allowed base ports. |
| Change machine recipe | Matching template keys preserve port IDs; removed ports cascade-delete links; new ports receive new IDs. |
| Delete node | Node, owned ports, and incident links are removed atomically. |
| Valid link | Output-to-input link is created with a stable ID. |
| Invalid direction | Input-to-input and output-to-output links are rejected. |
| Cardinality | Second outgoing or incoming link is rejected; no link is replaced implicitly. |
| Same-node link | Link between ports on one node is rejected. |
| Cycle | Structurally valid directed cycle is accepted by the graph domain. |
| Disabled node | Disabling a node preserves its ports and links. |
| Invalid position | NaN and infinity positions are rejected without mutation. |
| Import valid graph | Valid graph retains IDs, array order, revision, and port-template bindings. |
| Import malformed graph | Duplicate IDs, orphan ports, missing link endpoints, and template mismatch reject without changing the active graph. |
| React Flow mapping | Domain IDs map one-to-one to node, handle, and edge IDs. |
| Command atomicity | Every rejected command leaves graph revision and all entity collections unchanged. |

---

## 14. Definition of Done for Contract v0.1

This contract is ready to govern implementation only when:

- [ ] The Design Baseline v1.0 is approved and its companion-specification governance patch is recorded.
- [ ] This contract is approved without unresolved authority conflicts.
- [ ] The Scenario and Content Contract exposes a deterministic `GraphCatalogResolver` boundary.
- [ ] All command types have unit tests for acceptance and rejection paths.
- [ ] All required acceptance fixtures pass.
- [ ] Structural validation report ordering is tested.
- [ ] Recipe-change port reconciliation is tested.
- [ ] Node-deletion and recipe-change cascades are tested.
- [ ] React Flow projection uses the same stable IDs as the domain graph.
- [ ] No link stores a free-form resource or rate override.
- [ ] No persisted graph command is implemented outside this command set.
- [ ] The Persistence Contract is created before durable user-save behavior is shipped.

---

## 15. Deferred Extensions

The following require later design work and must not be smuggled into v0.1 implementation:

| Deferred capability | Required future authority |
|---|---|
| Splitters, mergers, buses | Routing and Port Cardinality Extension |
| Buffers, tanks, storage | Storage and Temporal State Contract |
| Priority routing, valves, control signals | Automation and Control Contract |
| Two-way or bottom/top ports | Graph Domain Contract revision |
| Node groups, subgraphs, templates | Graph Organization Contract |
| Undo/redo and transactions | Command History Contract |
| Collaborative editing | Concurrency and Conflict Resolution Contract |
| Routed power, batteries, local grids | Power Network Contract |
| Dynamic time and maintenance | Temporal Simulation Contract |

---

## Appendix A. Reference Type Summary

```ts
export interface ProductionGraph {
  schemaVersion: 1;
  graphId: GraphId;
  revision: number;
  nodes: ProductionNode[];
  ports: ProductionPort[];
  links: ProductionLink[];
}

export interface ProductionPort {
  id: PortId;
  nodeId: NodeId;
  templateKey: string;
  role: PortRole;
  direction: PortDirection;
  side: PortSide;
  displayOrder: number;
  streamBindingKey: string | null;
}

export interface ProductionLink {
  id: LinkId;
  fromPortId: PortId;
  toPortId: PortId;
}
```

## Appendix B. Terms

| Term | Meaning |
|---|---|
| Canonical array order | Persistent order of a graph entity array after validated import and command application. |
| Materialized port | Persisted port entity created from a resolved content template so links have stable endpoint identity. |
| Port template | Catalog-owned semantic definition of a node port. |
| Stream binding | Stable content key connecting a port to a source, recipe, sink, or objective stream slot. |
| Structural validity | Validity of graph identity, references, directions, cardinality, and template consistency; not economic usefulness. |
| Soft production failure | An economically bad or useless operational outcome that remains structurally representable. |
| Graph command | The only approved persistent graph mutation mechanism in v0.1. |
| Projection | A React Flow representation derived from authoritative `ProductionGraph` state. |

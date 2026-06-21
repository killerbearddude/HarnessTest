# Crushline: Design and Production Systems Baseline v1.0

**Status:** Design Baseline v1.0

**Recommended repository path:** `docs/crushline-design.md`

**Primary stack:** React, TypeScript, Vite, React Flow, Zustand, Vitest, and Playwright

**Optional performance layer:** C++17 compiled to a suitable target only after measured need

**Genre:** Node-graph production sandbox / expert-pack progression puzzle

**Document purpose:** Canonical full-product and production-systems baseline. This document captures the game vision, system authority, long-term economy, progression, victory framework, and production rules. It is not a scenario-specific balance sheet or an executable implementation contract.

## 1. Document Authority and Boundary

This is the authoritative v1.0 design baseline for Crushline. It replaces any prior architecture language that depended on WPL, WNG, Godot, or a custom engine. Crushline is a React and TypeScript product first. C++17 is an optional pure-computation layer only when profiling proves the TypeScript implementation is a real bottleneck.

| This document defines | This document intentionally does not define |
| --- | --- |
| Product identity and player promise | Exact recipe rates or final balance values |
| Core graph/failure philosophy | Scenario-specific fixture graphs |
| System authority and data ownership | Formal evaluator implementation algorithm |
| Long-term production economy and upgrade model | Exact port templates for each machine |
| Victory framework and content roadmap | Final temporal simulation parameters |
| Technical architecture and optional native boundary | Low-level UI behavior or visual style guide |
| Required companion specifications | The prior prototype or early proof-of-concept contract |

A prior proof-of-concept may exist, but it is not restated in this baseline. This document does not use a short prototype stage as its organizing structure.

## 2. Executive Summary

Crushline is a node-graph production sandbox where players solve large, interconnected production problems by assembling industrial systems from machines, resources, energy capacity, waste handling, recovery loops, and progression unlocks. The graph is the factory.

The game is inspired by expert Minecraft modpack progression: long dependencies, alternate routes, bottlenecks, coupled outputs, dirty shortcuts, recovered byproducts, and the satisfaction of turning early problems into late-game opportunities.

The endgame is not a single prescribed recipe chain. The player assembles a Closed-Line Seed and proves that the surrounding industrial graph can remain stable, recoverable, repairable, and sufficiently independent under certification conditions. Multiple material economies and industrial philosophies may satisfy the same functional requirements.

| Area | v1.0 decision |
| --- | --- |
| Product promise | A deep, graph-first industrial progression sandbox where solutions are authored rather than prescribed. |
| Core player activity | Build, inspect, repair, optimize, and evolve production graphs. |
| Technical direction | React/TypeScript application with React Flow graph interaction and a domain graph model as source of truth. |
| Simulation philosophy | Deterministic, explainable, conservation-safe simulation with failure as information. |
| Long-term victory | Closed-Line Certification and assembly of a Closed-Line Seed through multiple valid functional routes. |

## 3. Product Identity and Player Promise

Crushline is a production-chain graph game where the player does not primarily place terrain buildings, belts, or pipes. Instead, the player creates the operating logic of an industrial system. A player chooses machines, recipes, routes, recovery systems, power strategy, and upgrades, then observes the consequences in a living graph.

The intended question is:

> I need to produce this advanced capability. What chain of resources, machines, chemistry, power, recovery, upgrades, and tradeoffs can get me there?

- The graph is the primary play space, not a secondary diagram.
- A graph can be structurally valid but economically poor, wasteful, starved, unstable, or unable to meet the current objective.
- Multiple paths should commonly lead to a valid outcome.
- Old systems should remain improvable, retrofittable, or useful for support/recovery routes.
- The player should learn from bad graphs instead of merely being blocked by them.

## 4. Design Pillars

### 4.1 The graph is the factory

Nodes represent machines, sources, sinks, processors, buffers, infrastructure, and later automation helpers. Ports represent deliberate connection points. Links represent intentional industrial relationships. The player graph is the production solution.

### 4.2 Failure is playable

Wrong resources, insufficient power, bottlenecks, unused outputs, unmanaged waste, and incompatible process choices are usually simulation outcomes, not editor errors. The game must clearly explain what happened and where the root cause originated.

### 4.3 Progression opens capability spaces

Unlocks must create new ways to solve problems: fluids, thermal processing, chemistry, recovery, gas handling, control, repair autonomy, and advanced materials. They must not only increase throughput numbers.

### 4.4 Multiple paths to completion

Important objectives should be condition-based. Different material families, process routes, and recovery strategies should satisfy equivalent functional needs with different costs and risks.

### 4.5 Byproducts become opportunity

Byproducts should evolve from early problem to mid-game recoverable stream to late-game valuable input wherever possible. This supports long-term graph evolution.

### 4.6 Player creativity is the reward

A scenario defines constraints and success conditions. The player defines the industrial graph. Exact-chain objectives are reserved for tutorials or deliberate challenge modes only.

## 5. Technical Direction

Crushline is built as a React and TypeScript application. It must use existing production tooling for UI, graph interaction, persistence, test automation, and build workflow rather than reconstructing a general-purpose engine.

| Layer | Responsibility |
| --- | --- |
| React | Application composition, panels, menus, inspectors, dialogs, state-driven UI. |
| React Flow | Canvas interaction, nodes, edges, pan/zoom, selection, dragging, connection gestures. |
| TypeScript domain model | Graph meaning, resources, machines, recipes, objectives, progression, diagnostics, persistence. |
| TypeScript evaluator | Reference simulation and content validation behavior. |
| Zustand | Shared application/game state slices. |
| Vite | Development and production build tooling. |
| Vitest and Playwright | Domain tests, regression fixtures, and browser interaction testing. |
| Optional C++17 module | Pure computation only after profiling proves the TypeScript evaluator is a user-visible bottleneck. |

No custom platform layer, custom renderer, custom graph-editor engine, custom input abstraction, or custom scene system is an active project goal.

### 5.1 Optional C++17 performance boundary

TypeScript is the default language for the game and reference evaluator. A C++ module may be introduced only after the TypeScript implementation exists, profiling identifies a specific bottleneck, test vectors exist, and a narrow input/output contract is stable. C++ is limited to C++17. It must not own UI state, React state, DOM behavior, save-file formatting, game presentation, or content authoring.

- Valid future candidates: high-volume graph evaluation, route optimization, batch simulation, or large content diagnostics.
- Invalid reasons to introduce C++: preference, aesthetic purity, or premature concern about hypothetical scale.
- Any native/Wasm implementation must match the TypeScript evaluator contract against shared fixtures.

## 6. Product Architecture and Authority Model

Crushline separates interaction, domain data, simulation, content, and persistence. React Flow is a visual interaction layer, not the authoritative game state.

Authoritative update path:

> User action -> domain graph command -> authoritative ProductionGraph update -> evaluator/diagnostics update -> React Flow projection -> UI render

| Layer | Owns | Must not own |
| --- | --- | --- |
| Graph UI adapter | React Flow nodes, edges, selection synchronization, viewport, interaction commands. | Resource creation, recipe authority, evaluator truth. |
| Production graph model | Node identity, selected machine/recipe, structural ports, links, enabled state, positions. | React component lifecycle or visual-only state. |
| Content catalog | Resource, machine, recipe, capability, upgrade, scenario, objective definitions. | Transient graph state. |
| Evaluator | Material flow, capacity, power ledger, diagnostics, objectives, route evidence. | Direct DOM/React manipulation. |
| Persistence | Validated save data, versioning, migrations, catalog/scenario references. | Deriving rules from unvalidated UI state. |

### 6.1 Authority rules

- Ordinary port templates derive from a node selected machine and recipe definition; they are not independently authored rate records.
- A graph link connects ports. It does not freely select, invent, or override a material.
- A source or recipe output determines what material is emitted on an output stream.
- A recipe output stream determines whether its output is primary, byproduct, waste, catalyst return, or another defined stream role.
- Waste and byproduct are stream roles, not immutable global properties of a resource.
- UI state may display derived information but must not become a second evaluator authority.

## 7. Graph Interaction Philosophy

### 7.1 Hard invalid operations

Hard invalid operations are graph structures the product cannot represent coherently or safely. They may be blocked by the graph UI or domain validator.

- Connecting a port to itself.
- Input-to-input or output-to-output connection where the port model does not allow it.
- Duplicate exact link.
- Link to a missing/deleted port.
- Violation of an explicit port cardinality constraint.
- Malformed imported graph or duplicate graph identity.

### 7.2 Soft production failures

Soft failures are valid graph structures that produce undesirable industrial outcomes. They remain visible, saveable, and editable.

- Wrong material connected to a process input.
- Missing required input.
- Insufficient power capacity.
- Unmanaged byproduct.
- Unused output.
- Contamination or reject stream from a defined recipe rule.
- Technically operating but inefficient route.

### 7.3 Connection policy

After structural validation passes, the graph should be permissive. Crushline should not block a connection merely because it is strategically poor or economically wrong. The evaluator owns its consequence.

## 8. Core Production System Model

### 8.1 Resource categories

The product treats materials as industrial streams rather than generic graph labels. The long-term catalog is organized by solid, fluid, and gas forms, with additional semantic classes for components, catalysts, and final modules. Power is a capacity ledger in the baseline model, not an ordinary free-form material selected on a link.

| Category | Meaning |
| --- | --- |
| Solid | Ores, ingots, powders, plates, components, machine parts. |
| Fluid | Water, acids, solutions, brine, oils, solvents, slurries. |
| Gas | Air, oxygen, nitrogen, hydrogen, steam, methane, chlorine, process gases. |
| Catalyst / service material | Materials consumed, recovered, or circulated to affect process behavior. |
| Component / module | Constructed intermediate used for upgrades, machines, control, or endgame certification. |

### 8.2 Node roles

| Node role | Purpose |
| --- | --- |
| Source | Introduces scenario-authorized material at defined capacity or availability. |
| Process machine | Transforms defined input streams into defined output streams according to a selected recipe. |
| Sink | Accepts an allowed stream for disposal, storage, neutralization, or defined handling. |
| Objective sink | Defines the delivery boundary used to measure objective completion. |
| Generator / infrastructure | Contributes to the power ledger or other scenario infrastructure without implying generic energy routing. |
| Future routing/control node | Introduces explicit splitting, merging, buffering, priority, signals, or automation when the system design supports it. |

### 8.3 Recipes and stream roles

A recipe is a transformation contract. It declares required machine compatibility, input streams, output streams, byproduct/waste streams, operating demand, and progression requirements. Output stream role is attached to the recipe output, not to the global resource definition.

| Stream role | Meaning |
| --- | --- |
| Primary | The intended product of a recipe. |
| Byproduct | A secondary output that may require handling or may become useful later. |
| Waste | A stream whose unmanaged accumulation or disposal may create a penalty. |
| Recovered | A stream intentionally returned to a usable process or recovery route. |
| Catalyst return | A recoverable or partially recoverable process aid. |

### 8.4 Conservation and capacity invariants

Every production implementation must preserve a conservation-safe relationship between input, capacity, output, byproduct, and power. A throughput upgrade cannot create additional output without a corresponding rule for input consumption and power demand. A graph link cannot create material that the upstream source or recipe output did not produce.

- Actual input consumption, primary output, byproduct output, and power demand must derive from the same effective capacity and run fraction.
- A produced stream is either delivered to a compatible downstream port, held by a future explicit buffer/storage system, reported as surplus, or handled by an allowed sink.
- The authoritative evaluator defines rate units and tolerance policy in a dedicated evaluator specification.
- Stable ordering, numeric epsilon use, and tie-breaking are implementation-contract concerns and must be specified before a solver change is accepted.

### 8.5 Baseline power model

Crushline v1.0 selects a global power-ledger model for the baseline steady-state production system. Generators contribute available capacity; enabled machines draw defined operating demand and, where applicable, explicitly defined standby demand. The evaluator calculates a deterministic power margin and applies a documented brownout policy. Power is displayed in the graph UI but is not initially modeled as a generic routed resource link.

Routed electrical networks, batteries, priority distribution, local grids, and dynamic demand spikes are future infrastructure systems. They require a dedicated power-network or temporal-simulation specification before implementation.

## 9. Objectives, Measurement, and Diagnostics

### 9.1 Objective measurement definitions

| Term | Definition |
| --- | --- |
| Produced | A recipe or source emits a material stream at a machine output. Production alone does not necessarily satisfy an objective. |
| Delivered | A required material reaches the designated objective sink at the required measured rate. |
| Handled | A stream reaches an approved sink, treatment process, recovery chain, or scenario-authorized destination. |
| Recovered | A previously byproduct/waste stream becomes a defined useful input or approved recovered resource. |
| Discarded | A stream reaches a disposal sink. It may count as handled only if the objective allows disposal. |
| Surplus | Produced output that is not consumed, delivered, stored, or handled by an approved destination. |

### 9.2 Diagnostics contract

Diagnostics are a first-class product system. The player must be able to identify root causes without reading internal evaluator logs. A diagnostic system must distinguish root causes from cascade symptoms and keep messages stable enough for test fixtures.

| Diagnostic field | Purpose |
| --- | --- |
| Diagnostic ID / message key | Stable identity for tests, localization, and deduplication. |
| Severity | Information, warning, failure, or blocking condition. |
| Causality | Root cause or cascade symptom. |
| Affected entity | Node, port, link, resource stream, objective, or scenario condition. |
| Observed and expected values | Rate, power, capacity, or state that explains the discrepancy. |
| Remediation hint | Actionable player-facing direction without prescribing the only solution. |

A wrong input should surface the wrong input as the root cause before downstream starvation, deficit, or objective failure messages.

## 10. Progression and Upgrade Economy

### 10.1 Capability-based progression

Progression is a web of capabilities rather than a linear number ladder. A capability unlock gives the player a new production option or operating behavior.

- Mechanical processing: crushing, sorting, washing, grinding, compacting.
- Fluid handling: water supply, dirty water, slurries, pumps, tanks.
- Thermal processing: smelting, roasting, calcination, alloying.
- Chemical processing: acids, catalysts, separation, neutralization.
- Waste management: treatment, filtering, recovery, recycling.
- Energy systems: generators, high-load machinery, stabilization.
- Automation: monitoring, routing, throttling, repeatable patterns.
- Advanced materials: high-grade alloys, precision components, controlled environments.

### 10.2 Machine upgrade principles

- Every upgrade changes at least two dimensions: throughput, yield, power, recipe compatibility, ports, byproducts, recovery, automation, stability, or failure behavior.
- Every new tier introduces an industrial dependency rather than merely a number increase.
- Basic machines remain useful for low-power, dirty, challenge, or support routes.
- In-place retrofits are preferred when they let old graphs evolve rather than be deleted.
- Graph-visible upgrades are preferred: added ports, recovery outputs, service inputs, control connections, or new route compatibility.

| Tier | Name | Primary role |
| --- | --- | --- |
| 0 | Makeshift | Crude, inefficient, limited compatibility. |
| 1 | Basic | First reliable production systems. |
| 2 | Reinforced | Higher throughput and tougher materials. |
| 3 | Sealed | Fluid, gas, pressure, and contamination control. |
| 4 | Chemical | Corrosive, caustic, acid-compatible processing. |
| 5 | Precision | Clean, controlled, high-yield processing. |
| 6 | Automated | Monitoring, control, stabilization, and graph behavior. |
| 7 | Closed-Line | Self-maintaining, recovery-aware, certification-ready systems. |

### 10.3 Node upgrade families

| Node type | Early role | Later evolution |
| --- | --- | --- |
| Splitter | Equal split from one input. | Priority, ratio, filtered, or signal-controlled distribution. |
| Merger | Combines compatible incoming streams. | Filtered, priority, contamination-aware merging. |
| Buffer | Stores surplus. | Threshold, reserve, signal-emitting, emergency behavior. |
| Sink | Destroys or accepts waste. | Recovery, neutralizing, scrubbing, regulated emissions behavior. |
| Monitor | Reports a rate or state. | Emits control signals and causal diagnostics. |
| Valve / pump | Manual or fixed flow behavior. | Backpressure, throttling, priority, and regulation. |
| Compressor | Simple gas compression. | Staged compression, heat recovery, pressure regulation. |
| Catalyst loop | Manual catalyst routing. | Recovery and loss-minimization behavior. |

## 11. Victory Framework: Closed-Line Certification

The final product fantasy is not simply manufacturing an artifact. The player proves that they have built a durable industrial organism: productive, recoverable, repairable, and sufficiently independent of unconstrained outside extraction.

### 11.1 Closed-Line Seed

The Closed-Line Seed is a packaged autonomous factory nucleus. It is assembled from certified functional modules and earns final significance only when the surrounding graph passes certification behavior.

| Functional module | What it proves | Example route families |
| --- | --- | --- |
| Structure | Durable bodies and final shell production. | Steel, aluminum, titanium, ceramic composite, recycled alloy. |
| Power | Stable operation across required operating conditions. | Steam stabilization, hydrogen cells, methane reforming, batteries, waste-to-power. |
| Control | Ability to observe and regulate system behavior. | Copper board, silicon logic, graphite relay matrix, recycled electronics, pneumatic/fluidic control. |
| Recovery | Value reclamation and accumulation prevention. | Filtering, neutralization, scrap recovery, gas scrubbing, catalyst recovery. |
| Chemistry | Advanced transformation capability. | Sulfuric, chlor-alkali, nitrogen, phosphate, solvent routes. |
| Atmosphere | Gas/process environment control. | Nitrogen, argon, oxygen, steam, vacuum/low-gas routes. |
| Water | Sustainable fluid process operation. | Water recovery, condensation, brine management, dirty-water treatment. |
| Repair | Maintenance autonomy during final operation. | Repair kits, cartridges, parts recovery, self-cleaning filters. |

### 11.2 Certification principles

- Final victory is condition-based, not exact-recipe-based.
- Each functional module may have multiple accepted route proofs.
- Waste, power, water, gas, repair, recovery, and final assembly all matter.
- Scenario pressure may change which route is convenient without making one material family universally dominant.
- Closed-Line Certification requires a later temporal simulation specification. It is not merely a larger version of the baseline steady-state evaluator.

## 12. Replayability and Route Identity

### 12.1 Scenario modifiers

| Modifier | Effect on play |
| --- | --- |
| Iron poor | Encourages aluminum, ceramic, titanium, or recycling-heavy structure routes. |
| Water scarce | Raises value of closed water loops, condensation, dry processing, and reuse. |
| Sulfur poor | Makes sulfuric chemistry less dominant; favors chlor-alkali, nitric, or caustic alternatives. |
| Rich scrap field | Makes recycling and dirty recovery routes more attractive. |
| Halite rich | Makes brine electrolysis, hydrogen, chlorine, and sodium hydroxide routes attractive. |
| Low power start | Favors efficiency, staged upgrades, and lower-demand machinery. |
| Waste regulation | Requires strict treatment, recovery, neutralization, or scrubber planning. |
| Machine limit | Rewards dense, precision, or high-throughput routes over sprawling systems. |
| Gas heavy | Encourages air separation, inert processing, and gas recovery loops. |

### 12.2 Route identities

| Route identity | Core materials | Strength | Weakness |
| --- | --- | --- | --- |
| Steel Leviathan | Iron, coal, limestone, steam. | Simple, robust, high throughput. | Dirty, high ore use, high emissions. |
| Salt Engine | Halite, brine, hydrogen, chlorine, sodium hydroxide. | Coupled useful outputs. | Can clog when outputs become unbalanced. |
| Waste Saint | Scrap, slurry, dirty water, carbon dioxide. | Low fresh-input dependency. | Complex routing and variable outputs. |
| Cold Line | Air, nitrogen, argon, oxygen, hydrogen. | High-grade materials and atmosphere control. | High power and machinery complexity. |
| Glass Knife | Silica, copper, acids, clean processing. | Efficient and precise. | Fragile and contamination-sensitive. |
| Black Loop | Coal, methane, graphite, hydrogen, carbon monoxide. | Strong reduction and energy chemistry. | Dirty gas handling and emissions. |

Route credits and route-equivalence scoring require a separate, auditable route-proof specification before they become player-facing scoring systems. The product baseline defines the route identities, not a premature scoring algorithm.

## 13. Long-Term Material Economy

The base catalog contains 36 long-term material roots: 12 solids, 12 gases, and 12 liquids. This is a content-framework target, not a requirement that every material appear in every scenario or release. Steam is treated as a process gas rather than described as an ambient-state material.

### 13.1 Solids

| Material | Primary role | Suggested progression band |
| --- | --- | --- |
| Iron Ore | Iron, steel, frames, machinery. | Early |
| Copper Ore | Wire, circuits, heat exchangers. | Early |
| Coal | Fuel, coke, reducing agent, carbon chemistry. | Early |
| Limestone | Flux, lime, cement, neutralization, scrubbing. | Early |
| Silica Sand | Glass, silicon, ceramics, filter media. | Early to mid |
| Bauxite | Alumina and aluminum route. | Mid |
| Sulfur | Sulfuric acid and sulfur chemistry. | Mid |
| Halite | Brine, chlorine, caustic chemistry, electrolysis. | Mid |
| Phosphate Rock | Phosphate chemistry and electrolyte routes. | Mid |
| Nickel Ore | Batteries, alloys, catalysts. | Mid to late |
| Ilmenite | Titanium intermediate and pigment route. | Late |
| Graphite | Electrodes, lubricants, batteries, high-temperature parts. | Late |

### 13.2 Gases

| Material | Primary role | Suggested progression band |
| --- | --- | --- |
| Air | Feedstock for separation and combustion processes. | Early to mid |
| Oxygen | Combustion, oxidation, smelting boost, acid production. | Early to mid |
| Nitrogen | Inerting, ammonia, controlled atmospheres. | Mid |
| Carbon Dioxide | Combustion byproduct, capture, carbonation, scrubbing. | Early to mid |
| Carbon Monoxide | Reducing gas, syngas, dirty metallurgy. | Mid |
| Hydrogen | Reduction, ammonia, fuel cells, hydrogenation. | Mid |
| Steam | Power, heat transfer, thermal processing. | Early |
| Methane | Fuel gas, reforming, hydrogen source. | Mid |
| Chlorine | Chlor-alkali chemistry, etching, disinfection. | Mid |
| Ammonia | Nitrogen chemistry, fertilizer, coolant route. | Mid |
| Sulfur Dioxide | Roasting byproduct, sulfuric acid precursor. | Mid |
| Argon | Inert high-grade metallurgy and precision processing. | Late |

### 13.3 Liquids

| Material | Primary role | Suggested progression band |
| --- | --- | --- |
| Water | Washing, steam, cooling, electrolysis. | Early |
| Dirty Water | Waste stream, filtration, recovery pressure. | Early |
| Brine | Chlorine, hydrogen, sodium hydroxide via electrolysis. | Mid |
| Crude Oil | Fuel, solvents, organic chemistry, residues. | Mid |
| Sulfuric Acid | Leaching, batteries, fertilizer, extraction. | Mid |
| Hydrochloric Acid | Cleaning, chloride chemistry, leaching. | Mid |
| Nitric Acid | Nitrates, oxidizer chemistry, etching. | Mid to late |
| Phosphoric Acid | Electrolyte, phosphate chemistry, corrosion control. | Mid |
| Sodium Hydroxide Solution | Neutralization, alumina refining, chemical processing. | Mid |
| Ammonia Solution | pH control, fertilizer, nitrogen chemistry. | Mid |
| Ethanol | Solvent, fuel additive, organic chemistry. | Mid |
| Hydrogen Peroxide | Bleaching, oxidation, advanced chemical recipes. | Late |

## 14. Intermediate Products and Components

The base materials are roots, not the whole economy. Crushline should create a broad but staged layer of processed materials, components, upgrade kits, and functional modules. This supports both machine construction and route diversity.

| Component family | Examples | Purpose |
| --- | --- | --- |
| Processed materials | Crushed ores, concentrates, dusts, slurries, solutions, ingots, plates, rods, glass, ceramics. | Bridge extraction to manufacturing. |
| Mechanical components | Gear sets, bearings, shafts, fasteners, frames, casings. | Make machines physical and upgradeable. |
| Fluid components | Pipes, valve banks, pump rotors, gaskets, liners, sealed tanks. | Support fluid, slurry, and chemical systems. |
| Gas components | Canisters, vessels, compressor stages, manifolds, scrubber cartridges, condenser coils. | Enable pressure and gas-control gameplay. |
| Electrical/control components | Wire, coils, motors, boards, sensors, actuators, signal buses. | Support monitoring and automation. |
| Chemical components | Filter media, activated carbon, lime, catalyst beds, electrolyte, oxidizer mix, neutral sludge. | Create chemistry and waste-processing depth. |
| Thermal components | Refractory brick, ceramic liner, burner assembly, heat exchanger, insulation. | Support high-temperature and heat-recovery routes. |
| Recovery components | Recovery manifolds, membrane stacks, catalyst loops, water/gas recovery loops. | Enable closed-loop play and certification. |
| Functional modules | Certified structure, power, control, recovery, chemistry, atmosphere, water, repair. | Assemble the Closed-Line Seed through route-equivalent systems. |

A mature full content pass may contain approximately 200 to 275 resources and components. This is a planning range, not an irreversible content commitment. Each content expansion must prove that it creates new route decisions, not merely recipe volume.

## 15. Content and Systems Sequencing

The roadmap is staged by system capability, not by a redefinition of the earlier prototype. Each pass adds a meaningful industrial decision layer and should be validated before the next pass expands the catalog.

| Pass | Focus | Primary additions |
| --- | --- | --- |
| A | Foundational production loop | Core extraction, basic processing, simple conversion, objective delivery, basic power ledger, first diagnostics. |
| B | Component economy | Plates, wire, gears, frames, pipes, media, casings, machine build inputs. |
| C | Reinforced machinery | Steel, bearings, refractory parts, reinforcement kits, durable machine upgrades. |
| D | Sealed fluid and gas systems | Gaskets, valves, pressure equipment, pumps, compressors, controlled process inputs. |
| E | Basic chemistry | Acid/base routes, chemical tanks, catalyst beds, corrosion-resistant systems, recovery byproducts. |
| F | Precision and automation | Sensors, circuits, control boards, actuators, smart buffers, monitors, routing control. |
| G | Closed-loop economy | Recovery manifolds, membranes, catalyst loops, water/gas recovery, repair chains. |
| H | Closed-Line Trial | Certified modules, scenario pressure, source-cutoff behavior, temporal certification, final Seed assembly. |

## 16. Persistence, Versioning, and Content Compatibility

Save/load is a product promise. The product must preserve a player graph even when it fails an objective. It must also be resilient to catalog and scenario evolution.

| Saved data category | Requirement |
| --- | --- |
| Save format version | Supports migration of structural save schema. |
| Catalog/content version | Identifies the resource, machine, recipe, upgrade, and capability catalog used by the save. |
| Scenario version | Identifies the scenario objective and constraints used to interpret the graph. |
| Graph state | Stable IDs, node kinds, selected machines/recipes, positions, enabled states, and links. |
| Progression state | Unlocked capabilities, completed milestones, upgrades, route evidence where applicable. |
| Viewport/UI state | Optional convenience state separate from domain truth. |
| Import validation | Duplicate IDs, missing definitions, invalid ports, invalid links, and obsolete content must be detected deterministically. |

Save migration behavior, catalog replacement policy, and invalid-import recovery require a dedicated persistence specification before content changes become live. A save version number by itself is insufficient.

## 17. Determinism, Testing, and Authoring Governance

Crushline must be explainable to players and stable for authors. Determinism is not only a programming preference; it is required for testable diagnostics, reproducible saves, route evaluation, balance comparisons, and content review.

- The evaluator must have stable graph ordering, deterministic tie-breaking, explicit numeric tolerance, and consistent diagnostic ordering.
- Each new machine, recipe, upgrade, scenario modifier, and objective must have authoring validation.
- Regression fixtures must cover successful routes, degraded routes, invalid imports, diagnostic causality, and save/load equivalence.
- Route diversity must be tested numerically across relevant scenario modifiers before a route is treated as strategically viable.
- A content addition that adds recipe count but no new decision pressure is not sufficient justification for inclusion.

## 18. Required Companion Specifications

This document is full product baseline v1.0. It intentionally delegates executable detail to companion specifications. No implementation area should be governed by invented rules simply because this product document is high-level.

| Companion specification | Required before |
| --- | --- |
| Evaluator and material-flow contract | Changing or implementing solver behavior, capacity rules, conversion, consumption, or conservation. |
| Power ledger and infrastructure contract | Implementing brownouts, standby draw, power margin, priority, buffering, or future routed power. |
| Scenario/content contract | Shipping a scenario, defining objective thresholds, balancing rates, or claiming route validity. |
| Diagnostic catalog and UX contract | Shipping player-facing failure guidance or causal diagnostic behavior. |
| Persistence and migration contract | Shipping durable saves, import/export, or catalog compatibility changes. |
| Temporal certification simulation contract | Implementing demand spikes, source cutoff, repair autonomy, time-based stability, or Closed-Line trial behavior. |
| Route proof and substitution contract | Awarding route credits, scoring alternate routes, or validating functional victory slots. |
| Visual/UI design system | Committing to final node visuals, navigation hierarchy, accessibility behavior, or production presentation. |

## 19. Non-Goals and Guardrails

- Do not rebuild a generic engine, renderer, graph-editor library, platform layer, or native runtime before the game proves a need.
- Do not introduce C++ without profiling and a stable pure-computation contract.
- Do not turn every wrong input into a bespoke exception; default outcomes must stay understandable and authored exceptions must earn their complexity.
- Do not expand content faster than diagnostics, balance validation, and player comprehension can support.
- Do not let Closed-Line Certification contaminate the steady-state production evaluator; temporal certification is a separate later system.
- Do not require all materials, route families, or advanced systems in every scenario or run.

## 20. Final Design Statement

Crushline is a graph-first industrial progression sandbox. Its central promise is not a single ideal factory. It is the experience of building an understandable but imperfect industrial system, learning from its failures, and evolving it into something more capable, more efficient, and more self-sustaining.

The final game should allow two players to solve the same certification problem through different industrial philosophies. One may build a dirty steel-heavy system, another a recycling network, another a gas-controlled precision line. Each should be legible, valid, and personally authored.

Crushline proves the game first: React and TypeScript build the product; React Flow builds the interaction surface; C++17 remains an optional optimization boundary. The product does not earn its identity from custom infrastructure. It earns it from the depth, clarity, and creativity of its production systems.

## Appendix A. Glossary

| Term | Meaning |
| --- | --- |
| Closed-Line Seed | Final artifact representing a portable autonomous industrial nucleus. |
| Closed-Line Certification | Condition-based endgame proof of stability, recovery, repair, resource security, and final assembly. |
| Functional victory slot | An endgame capability that may be fulfilled through multiple material routes. |
| Route identity | A recognizable industrial philosophy defined by its material families, strengths, and tradeoffs. |
| Produced | Emitted by a source or machine output. |
| Delivered | Received by a designated objective sink and eligible to satisfy an objective. |
| Handled | Accepted by an authorized sink, treatment, or recovery process. |
| Recovered | Returned from a waste/byproduct stream into approved useful production. |
| Primary/byproduct/waste stream | Recipe-output role; not a permanent global property of a resource. |
| Power margin | Available power capacity minus defined demand, expressed by the applicable power contract. |
| Root-cause diagnostic | The earliest actionable explanation for a failure, distinct from downstream symptoms. |
| Temporal certification | Future time-based simulation used for stability trials, source cutoff, demand spikes, and repair autonomy. |

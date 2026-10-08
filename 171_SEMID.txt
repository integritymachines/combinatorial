171_SEMID.txt

SEMID — Semiconductor Development
v0.1 | 8 October 2026 | Problem layer

SCOPE
Macro Domain anchor: #TRANS. Primary Domain: 102 #PROD. Industry: ##SEMICONDUCTOR. Territory: #DEVELOPMENT.
Split-from reference: 170 SEMIM.
New semiconductor hardware definitions, circuit and package implementation, physical test capability and silicon product validation define this territory. It includes discrete architecture, netlist, geometry, interconnect and test-content decisions.
Manufacturing capability, reticle preparation and routine fabrication, assembly, inspection, test and device repair remain SEMIM. Standalone supply commitments, movement, workforce arrangements, utilities, commercial offers and installed digital-resource operation remain with SCM, LOG, HR, ENER, MKT and COMP when those contracts define the decision.

#design | 1##

SEMID101 Semiconductor Architecture Configuration.
DESCRIPTION Select hardware blocks, memory organizations, process options and integration schemes that meet semiconductor product requirements within power, performance, area and cost limits.
TEMPLATE Architecture exploration and hardware cost modeling | Mixed-discrete design-space optimization with analytical models and simulation.
REGIME #design | Commits a new hardware architecture before circuit implementation.
STRUCTURE #select + #map | Selects physical implementation options and assigns them to hardware subsystems.
PRIORITY Critical | Architecture sets the feasible product implementation space.
RELEVANCE Critical | Better choices affect product capability, silicon cost and development investment.
HARDNESS High | Discrete implementation choices interact with uncertain workload, yield and packaging models.
DEPENDENCIES ∅ → SEMID101 → SEMID102, SEMID105, SEMID108, SEMID111.
TAGS #TRANS #PROD ##SEMICONDUCTOR #DEVELOPMENT #design #select #map ##architecture ##design-space ##chiplet ##memory.
COMMENTS Includes physical redundancy capacity choices. Allocation of repair spares to defects in fabricated devices remains SEMIM.

SEMID102 High-Level Hardware Synthesis.
DESCRIPTION Choose hardware resources and assign behavioral operations to resources and clock steps under data dependencies, latency and implementation limits.
TEMPLATE Datapath and controller synthesis | Scheduling-and-binding ILP; list scheduling and resource-sharing heuristics.
REGIME #design | Defines a hardware implementation and its cycle-level behavior.
STRUCTURE #map + #place + #select | Assigns operations to functional units, places them in clock steps and selects resource instances.
PRIORITY High | Behavioral synthesis recurs in accelerator and specialized datapath development.
RELEVANCE High | Better sharing and cycle assignments improve hardware area and throughput.
HARDNESS High | Resource sharing, chaining and control conditions couple allocation and cycle timing.
DEPENDENCIES SEMID101 → SEMID102 → SEMID103.
TAGS #TRANS #PROD ##SEMICONDUCTOR #DEVELOPMENT #design #map #place #select ##high-level-synthesis ##binding ##schedule ##precedence.
COMMENTS Clock-step placement defines circuit behavior. It is not a factory or installed-compute execution schedule.

SEMID103 Logic Network Restructuring.
DESCRIPTION Choose an equivalent logic network that meets circuit area and depth requirements while preserving the specified Boolean behavior.
TEMPLATE Technology-independent logic synthesis | AIG rewriting, refactoring and balancing; equivalence-constrained resynthesis.
REGIME #design | Defines circuit logic before or alongside library implementation.
STRUCTURE #link + #select | Constructs logic connections and selects replacement subcircuits under functional equivalence.
PRIORITY Critical | Logic optimization is a central digital implementation step.
RELEVANCE High | Better networks reduce implementation area and timing pressure.
HARDNESS High | Local rewrites interact through shared logic and downstream physical cost.
DEPENDENCIES SEMID102, SEMID901 → SEMID103 → SEMID104.
TAGS #TRANS #PROD ##SEMICONDUCTOR #DEVELOPMENT #design #link #select ##logic-synthesis ##boolean-network ##aig ##equivalence.

SEMID104 Circuit Retiming.
DESCRIPTION Move register boundaries through a synchronous circuit to meet cycle-time and register-count requirements while preserving sequential behavior.
TEMPLATE Pipeline balancing and register retiming | Difference-constraint and minimum-cost-flow retiming; constrained integer extensions.
REGIME #design | Defines the register distribution of a circuit implementation.
STRUCTURE #place | Positions register boundaries along the supplied circuit graph under retiming equivalence laws.
PRIORITY High | Pipeline balancing recurs in timing-constrained synchronous circuits.
RELEVANCE High | Better boundaries improve clock period and register use.
HARDNESS Medium | Classical models have efficient algorithms; resets, enabled registers and physical timing complicate deployment | Polynomial-time for classical minimum-period and minimum-state retiming.
DEPENDENCIES SEMID103 → SEMID104 → SEMID107.
TAGS #TRANS #PROD ##SEMICONDUCTOR #DEVELOPMENT #design #place ##retiming ##registers ##sequential-equivalence.

SEMID105 Analog Circuit Topology Synthesis.
DESCRIPTION Choose analog building blocks and their connections to meet electrical specifications under device, power and area limits.
TEMPLATE Analog topology selection and simulation-based design exploration | Hierarchical mixed-discrete evolutionary synthesis with SPICE evaluation.
REGIME #design | Commits an analog circuit topology before physical layout.
STRUCTURE #link + #select | Constructs circuit connections and selects participating devices or building blocks.
PRIORITY Medium | Topology synthesis applies to analog and mixed-signal circuit development.
RELEVANCE High | Better topologies expand attainable performance and reduce redesign.
HARDNESS High | Topology choices require expensive electrical evaluation across process and operating conditions.
DEPENDENCIES SEMID101 → SEMID105 → SEMID114.
TAGS #TRANS #PROD ##SEMICONDUCTOR #DEVELOPMENT #design #link #select ##analog ##topology ##mixed-discrete ##simulation-optimization.
COMMENTS Pure continuous device sizing on a fixed topology falls outside this combinatorial Problem.

SEMID106 Standard-Cell Layout Synthesis.
DESCRIPTION Choose transistor folds and place and connect transistors within a reusable standard cell under cell-height, pin-access and fabrication rules.
TEMPLATE Transistor-level cell-library layout generation | Joint folding and placement search with SAT/SMT in-cell routing.
REGIME #design | Defines the physical layout of a new library cell.
STRUCTURE #place + #link + #select | Positions transistors, constructs intra-cell conductors and selects fold configurations.
PRIORITY Medium | Cell-layout generation is central to library and technology development.
RELEVANCE High | Better cell geometry improves density and pin access across many designs.
HARDNESS High | Folding, diffusion sharing, pin access and restrictive rules require tailored search.
DEPENDENCIES ∅ → SEMID106 → SEMID107, SEMID118, SEMID119.
TAGS #TRANS #PROD ##SEMICONDUCTOR #DEVELOPMENT #design #place #link #select ##standard-cell-synthesis ##transistor-folding ##sat ##smt.

SEMID107 Technology Mapping.
DESCRIPTION Cover circuit logic with compatible library cells under functional, area and timing requirements.
TEMPLATE Library-aware gate implementation | Cut-based DAG covering and dynamic programming; timing-aware mapping search.
REGIME #design | Commits the library realization of circuit logic.
STRUCTURE #map + #select | Assigns logic portions to cell realizations and selects a compatible implementation cover.
PRIORITY Critical | Digital circuits need an implementation in the target library.
RELEVANCE High | Better covers improve area, power and timing before physical closure.
HARDNESS High | Shared logic, multiple cell choices and physical cost make local covers interact.
DEPENDENCIES SEMID104, SEMID106, SEMID901 → SEMID107 → SEMID108, SEMID110, SEMID111, SEMID112, SEMID113, SEMID115, SEMID117.
TAGS #TRANS #PROD ##SEMICONDUCTOR #DEVELOPMENT #design #map #select ##technology-mapping ##library-cells ##dag ##covering.

SEMID108 Circuit Partitioning and Die Assignment.
DESCRIPTION Assign circuit components to hierarchical blocks or physical dies under balance, interface, timing and implementation-cost limits.
TEMPLATE Hierarchical netlist partitioning and chiplet decomposition | Constrained multilevel hypergraph partitioning; cost-aware technology-assignment search.
REGIME #design | Commits circuit boundaries before block or die implementation.
STRUCTURE #map + #select | Assigns components to blocks or dies and selects die technologies when those options are variable.
PRIORITY High | Partitioning supports large hierarchical and multi-die implementations.
RELEVANCE Critical | Die boundaries and technology choices can materially change product cost and performance.
HARDNESS High | Interface reach, balance, timing and heterogeneous die costs require iterative partition and geometry checks.
DEPENDENCIES SEMID101, SEMID107 → SEMID108 → SEMID109, SEMID115.
TAGS #TRANS #PROD ##SEMICONDUCTOR #DEVELOPMENT #design #map #select ##partition ##hypergraph ##chiplet ##technology-assignment.
COMMENTS For a fixed block set and fixed technologies, the decision assigns components to blocks only.

SEMID109 On-Chip Interconnect Topology Synthesis.
DESCRIPTION Select routers and physical interconnects that satisfy specified hardware communication demands within bandwidth, latency, area and power limits.
TEMPLATE Application-specific NoC architecture synthesis | Topology-and-routing MILP with hierarchical or heuristic decomposition.
REGIME #design | Defines a new on-chip communication circuit.
STRUCTURE #link + #select + #map | Constructs router links, selects router instances and assigns hardware endpoints to interfaces.
PRIORITY Medium | Custom NoC synthesis is central to communication-intensive SoCs.
RELEVANCE High | Better topology reduces communication bottlenecks and interconnect power.
HARDNESS High | Bandwidth, latency, topology and physical feasibility couple many alternative interconnects.
DEPENDENCIES SEMID108 → SEMID109 → SEMID115, SEMID121.
TAGS #TRANS #PROD ##SEMICONDUCTOR #DEVELOPMENT #design #link #select #map ##noc ##topology ##network ##connectivity.
COMMENTS Live traffic or application placement on an installed digital network belongs to COMP.

SEMID110 Power-Domain Configuration.
DESCRIPTION Assign hardware blocks to voltage and power domains and select required isolation, retention and level-shifting interfaces under operating-mode and timing requirements.
TEMPLATE Multivoltage and power-intent engineering | Discrete voltage-domain assignment ILP; partitioned optimization with timing checks.
REGIME #design | Defines circuit power domains and their implementation interfaces.
STRUCTURE #map + #select | Assigns blocks to power domains and selects interface implementations.
PRIORITY High | Power-domain design recurs in power-constrained SoCs.
RELEVANCE High | Better domain assignments reduce power and interface overhead.
HARDNESS High | Timing, mode compatibility and domain crossings constrain discrete choices.
DEPENDENCIES SEMID107 → SEMID110 → SEMID115, SEMID118, SEMID120.
TAGS #TRANS #PROD ##SEMICONDUCTOR #DEVELOPMENT #design #map #select ##voltage-islands ##power-domains ##low-power.

SEMID111 Testability Architecture Configuration.
DESCRIPTION Select scan, compression, built-in self-test, memory-repair and test-access structures under coverage, test-time, area and interface requirements.
TEMPLATE Hierarchical design-for-test and memory-test architecture | Discrete architecture exploration with test-cost, coverage and physical-feasibility evaluation.
REGIME #design | Defines the test capability built into the semiconductor product.
STRUCTURE #select + #map + #link | Selects test structures, assigns circuits to them and constructs test-access connections.
PRIORITY Critical | Test architecture determines whether complex products can be tested economically.
RELEVANCE Critical | Better testability affects test cost, defect detection and product yield.
HARDNESS High | Coverage, compression, power and physical overhead constrain many architecture alternatives.
DEPENDENCIES SEMID101, SEMID107 → SEMID111 → SEMID112, SEMID113, SEMID125, SEMID126.
TAGS #TRANS #PROD ##SEMICONDUCTOR #DEVELOPMENT #design #select #map #link ##dft ##test-compression ##mbist ##test-access.

SEMID112 Test-Point Selection and Assignment.
DESCRIPTION Select control and observation points and assign their test functions to improve circuit testability within area, timing and physical-overhead limits.
TEMPLATE Fault-coverage and physical-aware test-point engineering | Testability-guided discrete insertion search with ATPG or LBIST evaluation.
REGIME #design | Commits test points in the product netlist before test generation.
STRUCTURE #select + #map | Selects circuit sites and assigns control or observation roles.
PRIORITY Medium | Test-point optimization recurs where baseline testability is insufficient.
RELEVANCE High | Better points improve coverage and reduce pattern burden.
HARDNESS High | Coverage gains interact with congestion, timing, leakage and test-point sharing.
DEPENDENCIES SEMID107, SEMID111 → SEMID112 → SEMID113, SEMID117, SEMID125.
TAGS #TRANS #PROD ##SEMICONDUCTOR #DEVELOPMENT #design #select #map ##test-points ##testability ##fault-coverage.

SEMID113 Scan-Chain Configuration.
DESCRIPTION Assign scan registers to chains and choose their connections under chain-length, clock-domain, routing and test-power limits.
TEMPLATE Physical-aware scan insertion and chain balancing | Constrained partitioning and path-stitching heuristics with local refinement.
REGIME #design | Defines the scan connections of the semiconductor product.
STRUCTURE #link + #map | Constructs scan paths and assigns registers to chains under valid clock and endpoint conditions.
PRIORITY High | Scan chains are a common digital testability implementation.
RELEVANCE High | Better chains reduce shift time, routing overhead and test-power pressure.
HARDNESS High | Chain balance, clock mixing and physical distances interact across many scan registers.
DEPENDENCIES SEMID107, SEMID111, SEMID112 → SEMID113 → SEMID117, SEMID125.
TAGS #TRANS #PROD ##SEMICONDUCTOR #DEVELOPMENT #design #link #map ##scan-chain ##paths ##partition ##test-power.
COMMENTS Scan reordering remains a design connection decision even when performed after placement.

SEMID114 Analog and Custom Block Layout Synthesis.
DESCRIPTION Place and connect analog or custom circuit devices and blocks under matching, symmetry, isolation and fabrication requirements.
TEMPLATE Constraint-driven analog and custom layout engineering | Hierarchical geometric placement and constraint-aware routing search.
REGIME #design | Defines a new custom circuit layout from a supplied netlist.
STRUCTURE #place + #link | Positions devices and blocks and constructs conductors under matching and connectivity laws.
PRIORITY High | Analog and mixed-signal products require specialized physical layouts.
RELEVANCE High | Better layouts reduce parasitic mismatch and integration failures.
HARDNESS High | Electrical constraints, geometric matching and parasitic coupling require specialized layout search.
DEPENDENCIES SEMID105 → SEMID114 → SEMID115.
TAGS #TRANS #PROD ##SEMICONDUCTOR #DEVELOPMENT #design #place #link ##analog-layout ##matching ##symmetry ##geometry.

SEMID115 Die and Package Floorplanning.
DESCRIPTION Place and orient circuit macros or dies and choose permitted block shapes within chip or package outlines under nonoverlap, interface, routing and thermal limits.
TEMPLATE Macro and multi-die physical planning | Hierarchical floorplan search, sequence-pair annealing or geometric MILP with physical evaluation.
REGIME #design | Commits product geometry before detailed placement and interconnect realization.
STRUCTURE #place + #select | Positions oriented blocks or dies and selects permitted shape configurations.
PRIORITY Critical | Floorplans constrain the main physical implementation stages.
RELEVANCE Critical | Better geometry affects die area, package cost and attainable performance.
HARDNESS High | Nonoverlap, shape, routing and thermal tradeoffs require iterative hierarchical search.
DEPENDENCIES SEMID107, SEMID108, SEMID109, SEMID110, SEMID114 → SEMID115 → SEMID116, SEMID117, SEMID119, SEMID120, SEMID123.
TAGS #TRANS #PROD ##SEMICONDUCTOR #DEVELOPMENT #design #place #select ##floorplan ##macro-placement ##chiplet ##nonoverlap.
COMMENTS Fixed-shape variants choose positions and orientations only. Three-dimensional integration is a floorplanning variant.

SEMID116 Chip Interface Pin and Bump Assignment.
DESCRIPTION Assign signals and power connections to permitted pin, pad or bump sites under interface, spacing, grouping and routing limits.
TEMPLATE I/O planning and chip-package interface co-design | Constrained assignment and pin-placement optimization with routing-cost refinement.
REGIME #design | Commits the physical interface of a chip or die.
STRUCTURE #map + #place | Assigns connections to interface sites and positions interface geometries when sites are variable.
PRIORITY High | Physical interface assignment recurs across chip and multi-die designs.
RELEVANCE High | Better interfaces reduce escape congestion and integration cost.
HARDNESS High | Signal groups, power delivery, pin access and package escape feasibility interact.
DEPENDENCIES SEMID115 → SEMID116 → SEMID121, SEMID123.
TAGS #TRANS #PROD ##SEMICONDUCTOR #DEVELOPMENT #design #map #place ##pin-assignment ##bumps ##io ##chip-package.

SEMID117 Standard-Cell Placement.
DESCRIPTION Place library-cell instances at legal chip sites under row, nonoverlap, region, timing and routing requirements.
TEMPLATE Global placement, legalization and detailed placement | Analytical placement followed by discrete legalization and local placement refinement.
REGIME #design | Commits physical cell positions in a new circuit layout.
STRUCTURE #place | Positions cell instances in the chip site and row geometry.
PRIORITY Critical | Cell placement is a central digital physical-design contract.
RELEVANCE Critical | Better placement affects timing, routing feasibility and silicon area.
HARDNESS Critical | Large instance sets and coupled density, timing and congestion require multistage approximate optimization.
DEPENDENCIES SEMID107, SEMID112, SEMID113, SEMID115, SEMID901 → SEMID117 → SEMID118, SEMID119, SEMID120, SEMID121, SEMID126.
TAGS #TRANS #PROD ##SEMICONDUCTOR #DEVELOPMENT #design #place ##placement ##legalization ##wirelength ##congestion.

SEMID118 Discrete Gate Sizing and Buffer Insertion.
DESCRIPTION Select library-cell sizes and buffer insertions for a supplied circuit implementation under timing, slew, capacitance, power and area limits.
TEMPLATE Physical synthesis and electrical timing closure | Timing-driven discrete resizing and buffering with iterative physical refinement.
REGIME #design | Commits cell implementations and buffer structure before design release.
STRUCTURE #select + #map + #link | Selects gate and buffer options, assigns them to circuit sites and constructs buffered connections.
PRIORITY Critical | Electrical closure recurs throughout physical implementation.
RELEVANCE High | Better choices reduce violations and unnecessary power or area.
HARDNESS High | Multiple timing corners, reconvergent paths and parasitic feedback couple local choices.
DEPENDENCIES SEMID106, SEMID110, SEMID117, SEMID901 → SEMID118 → SEMID119, SEMID121.
TAGS #TRANS #PROD ##SEMICONDUCTOR #DEVELOPMENT #design #select #map #link ##gate-sizing ##buffering ##timing-closure ##multi-corner.

SEMID119 Clock Distribution Synthesis.
DESCRIPTION Choose clock-distribution connections, buffers and branch positions under skew, latency, slew, load, power and routing requirements.
TEMPLATE Clock-tree and clock-network engineering | Buffered tree synthesis with sink clustering, geometric embedding and timing refinement.
REGIME #design | Defines the physical clock distribution of a new circuit.
STRUCTURE #link + #select + #place | Constructs clock branches, selects buffers and positions branch or buffer sites.
PRIORITY Critical | Synchronous circuits depend on feasible clock distribution.
RELEVANCE High | Better networks improve timing margin and reduce clock power.
HARDNESS High | Skew, electrical loading, obstacles and multiple timing conditions couple topology and geometry.
DEPENDENCIES SEMID106, SEMID115, SEMID117, SEMID118, SEMID901 → SEMID119 → SEMID121.
TAGS #TRANS #PROD ##SEMICONDUCTOR #DEVELOPMENT #design #link #select #place ##clock-tree ##clock-network ##skew ##tree.

SEMID120 Power Delivery Network Design.
DESCRIPTION Choose on-chip power conductors, layers, vias and grid configurations under connectivity, voltage-drop, current-density and routing-space limits.
TEMPLATE Power-grid engineering with electrical signoff evaluation | Region-grid pattern search with circuit analysis; annealing or learned pattern assignment.
REGIME #design | Defines power-delivery structure within a new product layout.
STRUCTURE #link + #place + #select | Constructs connected power conductors, positions grid elements and selects layers or via configurations.
PRIORITY Critical | Physical circuits need feasible power delivery.
RELEVANCE High | Better grids reduce voltage loss and excess metal consumption.
HARDNESS High | Electrical reliability and signal-routing competition couple discrete grid choices.
DEPENDENCIES SEMID110, SEMID115, SEMID117, SEMID901 → SEMID120 → SEMID121, SEMID126.
TAGS #TRANS #PROD ##SEMICONDUCTOR #DEVELOPMENT #design #link #place #select ##pdn ##power-grid ##connectivity ##ir-drop ##electromigration.

SEMID121 Chip Global Routing.
DESCRIPTION Choose coarse net routes and routing-layer use under connectivity, regional capacity, timing and wirelength requirements.
TEMPLATE Congestion-driven global interconnect planning | Steiner-tree generation, maze routing and negotiated-congestion refinement.
REGIME #design | Defines chip interconnect guides before track-level realization.
STRUCTURE #link + #map | Constructs coarse connected net paths and assigns their segments to routing layers.
PRIORITY Critical | Global routing coordinates chip-wide interconnect demand.
RELEVANCE High | Better guides reduce congestion and downstream routing failures.
HARDNESS Critical | Many competing nets and limited routing capacities require decomposition and iterative congestion repair.
DEPENDENCIES SEMID109, SEMID116, SEMID117, SEMID118, SEMID119, SEMID120, SEMID901 → SEMID121 → SEMID122.
TAGS #TRANS #PROD ##SEMICONDUCTOR #DEVELOPMENT #design #link #map ##global-routing ##steiner-tree ##congestion ##layers.

SEMID122 Chip Detailed Routing.
DESCRIPTION Choose conductor paths, tracks and vias that realize chip nets under pin-access, spacing, layer and electrical rules.
TEMPLATE Track-level interconnect realization and design-rule closure | Pin-access and track-assignment optimization; maze routing with search and repair.
REGIME #design | Commits the final physical chip interconnect geometry.
STRUCTURE #link + #place + #select | Constructs connected conductor paths, positions them on tracks and selects via implementations.
PRIORITY Critical | Detailed routes are required for a manufacturable chip layout.
RELEVANCE Critical | Better realization can determine whether a product meets release requirements.
HARDNESS Critical | Dense pin access, complex rules and interacting nets require iterative search and repair.
DEPENDENCIES SEMID121, SEMID901 → SEMID122 → SEMID124, SEMID125, SEMID901.
TAGS #TRANS #PROD ##SEMICONDUCTOR #DEVELOPMENT #design #link #place #select ##detailed-routing ##pin-access ##vias ##design-rules.

SEMID123 Package Interconnect Routing.
DESCRIPTION Choose package, interposer or redistribution-layer connections under pin escape, layer, spacing, length-matching and signal-integrity requirements.
TEMPLATE Chip-package interconnect and escape-routing engineering | Network-flow or topological routing with pin reassignment and geometric refinement.
REGIME #design | Defines a new package interconnect layout.
STRUCTURE #link + #place + #map | Constructs conductors, positions their physical paths and assigns nets to layers or variable interface sites.
PRIORITY High | Package routing is central to packaged and multi-die products.
RELEVANCE High | Better routes reduce layer cost and package integration failures.
HARDNESS High | Dense escapes, cross-die timing and layer constraints require specialized routing methods.
DEPENDENCIES SEMID115, SEMID116, SEMID901 → SEMID123 → SEMID301, SEMID901.
TAGS #TRANS #PROD ##SEMICONDUCTOR #DEVELOPMENT #design #link #place #map ##package-routing ##rdl ##interposer ##escape-routing.

SEMID124 Layout Density Fill Optimization.
DESCRIPTION Select and place nonfunctional fill shapes in a product layout under density, spacing and parasitic-coupling requirements.
TEMPLATE Design-for-manufacturability layout finishing | Geometric fill insertion with density and coupling optimization; rule-based fill baseline.
REGIME #design | Defines manufacturable product geometry before release.
STRUCTURE #place + #select | Positions fill shapes and selects permitted shape and layer alternatives.
PRIORITY Medium | Density fill is required in technology flows with minimum-density rules.
RELEVANCE High | Better fill meets manufacturing rules with less parasitic and timing impact.
HARDNESS Medium | Rule-driven insertion is established; dense windows and electrical coupling require careful refinement.
DEPENDENCIES SEMID122 → SEMID124 → SEMID301, SEMID901.
TAGS #TRANS #PROD ##SEMICONDUCTOR #DEVELOPMENT #design #place #select ##metal-fill ##density ##dfm ##parasitics.

SEMID125 Physical Circuit Test Pattern Optimization.
DESCRIPTION Generate and retain circuit test stimuli that meet physical fault-detection requirements within pattern-count, tester-data and shift or capture power limits.
TEMPLATE Fault-model ATPG and test-set compaction | Constraint-based test generation, fault simulation and coverage-driven pattern compaction.
REGIME #design | Defines physical fault-test content before repeated device testing.
STRUCTURE #select + #map | Selects retained patterns and assigns logic values to controllable test inputs.
PRIORITY Critical | Physical fault-test content is central to digital product release.
RELEVANCE High | Better pattern sets reduce test cost and defect escape.
HARDNESS High | Fault activation, propagation, compression and unknown states constrain pattern generation and reduction.
DEPENDENCIES SEMID111, SEMID112, SEMID113, SEMID122, SEMID901 → SEMID125 → SEMID126, SEMID301.
TAGS #TRANS #PROD ##SEMICONDUCTOR #DEVELOPMENT #design #select #map ##atpg ##fault-coverage ##test-compaction ##test-power.
COMMENTS Defines physical device fault tests. It does not include general software verification or manufacturing test calendars.

SEMID126 Embedded Test Access and Protocol Design.
DESCRIPTION Assign cores or memories to test-access resources and place test sessions within a repeatable device test protocol under bandwidth, power and thermal limits.
TEMPLATE Core-wrapper and MBIST grouping with test-session design | Resource-constrained scheduling or packing with access assignment; physical grouping heuristics.
REGIME #design | Defines an embedded or repeatable product test protocol before routine test execution.
STRUCTURE #map + #place | Assigns test subjects to access or controller groups and positions their sessions in protocol time.
PRIORITY High | Integrated test protocols recur in multi-core and memory-rich products.
RELEVANCE High | Better access and concurrency reduce test time within power limits.
HARDNESS High | Access sharing, unequal durations and thermal or power limits couple grouping and session timing.
DEPENDENCIES SEMID111, SEMID117, SEMID120, SEMID125 → SEMID126 → SEMID301.
TAGS #TRANS #PROD ##SEMICONDUCTOR #DEVELOPMENT #design #map #place ##tam ##mbist ##protocol ##schedule ##power-constrained.
COMMENTS Protocol time is internal to a device test definition. Scheduling products on production testers remains SEMIM.

#plan | 3##

SEMID301 Silicon Validation Test Selection.
DESCRIPTION Select and prioritize physical silicon validation tests within available validation effort, using product requirements and observed failures.
TEMPLATE Requirement-driven post-silicon validation and adaptive test refinement | Failure-data-driven test ranking and constrained subset selection.
REGIME #plan + #adapt | Commits a validation campaign and revises its content when silicon evidence changes.
STRUCTURE #select + #place | Chooses validation tests and positions them in a priority order.
PRIORITY High | First-silicon validation supports release of new semiconductor products.
RELEVANCE Critical | Better selection reduces release delay and the risk of costly design escapes.
HARDNESS High | Rare failures, uncertain test value and limited validation effort require adaptive prioritization.
DEPENDENCIES SEMID123, SEMID124, SEMID125, SEMID126, SEMID901 → SEMID301 → SEMID901.
TAGS #TRANS #PROD ##SEMICONDUCTOR #DEVELOPMENT #plan #adapt #select #place ##post-silicon ##validation ##test-selection ##adaptive-testing.

#adapt | 9##

SEMID901 Semiconductor Engineering Change Optimization.
DESCRIPTION Revise a committed circuit or layout to meet changed functional or electrical requirements under frozen-layer, spare-resource and disruption limits.
TEMPLATE Functional and physical ECO with incremental signoff | Equivalence-constrained rectification; spare-cell matching and iterative MILP with local rerouting.
REGIME #adapt | Revises existing product-definition commitments after a material defect or requirement change.
STRUCTURE #select + #map + #link + #place | Selects edits, assigns replacement or spare cells, changes connections and revises permitted geometry.
PRIORITY High | Late product-definition changes recur in semiconductor programs.
RELEVANCE Critical | Better edits can avoid full redesign and reduce respin or remasking cost.
HARDNESS High | Frozen geometry, scarce spares, timing and functional equivalence constrain feasible local changes.
DEPENDENCIES SEMID122, SEMID123, SEMID124, SEMID301 → SEMID901 → SEMID103, SEMID107, SEMID117, SEMID118, SEMID119, SEMID120, SEMID121, SEMID122, SEMID123, SEMID125, SEMID301.
TAGS #TRANS #PROD ##SEMICONDUCTOR #DEVELOPMENT #adapt #select #map #link #place ##eco ##rectification ##spare-cells ##incremental-design.
COMMENTS Metal-only variants retain fixed cell positions and restrict changes to permitted conductors and spare resources.

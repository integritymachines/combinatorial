PROC (Continuous and Batch Process Manufacturing Systems) ========================================================

Scope: Continuous and batch process industries including chemicals, pharmaceuticals, food and beverage, refining, and polymers. Discrete manufacturing (parts, assembly) is explicitly excluded (handled under PROD). Focus is on combinatorial and mixed-integer decisions (e.g., topology, campaign sequencing, recipe-unit assignment, STN/RTN scheduling), not continuous control, simulation, or purely continuous convex programs.

1) DESIGN

PROC01 Process Network Synthesis & Topology Design 
Description: Selects and interconnects processing units, pipelines, headers, and storage to meet capacity and product slate targets under capital constraints.
Template: Multisite facility location / network flow with fixed charges | MINLP, MIP decomposition.
Relevance: Priority: Critical | Capital-intensive decisions defining plant topology and simultaneous transfer capabilities in refineries and bulk chemicals.
Hardness: Class: NP-hard | Generalizes fixed-charge network design and facility location.
Dependencies: Upstream: — | Downstream: PROC02, PROC03, PROC06.
Comments: Long-term structural choices that bound all physical operations | #des #config ##network-design ##piping

PROC02 Discrete Equipment Selection & Sizing 
Description: Selects the type, number, and discrete size capacities of reactors, columns, or processing units from standard industrial offerings.
Template: Capacity expansion / discrete sizing | MINLP, MIP.
Relevance: Priority: High | Major capital expenditure that strictly dictates downstream operational bottlenecks.
Hardness: Class: NP-hard | Involves discrete choice with non-linear cost and scale functions.
Dependencies: Upstream: PROC01 | Downstream: PROC04, PROC05, PROC18.
Comments: Often solved under multi-period demand uncertainty | #des #invest ##equipment-sizing ##capacity

PROC03 Tank Farm Configuration 
Description: Decides the number, capacities, and dedicated vs. flexible status of intermediate and final product storage tanks.
Template: Bin packing / discrete capacity planning | MINLP, MIP.
Relevance: Priority: High | Intermediate storage is the primary structural buffer in continuous/batch plants.
Hardness: Class: NP-hard | Combinatorial matching of product families to tank geometries.
Dependencies: Upstream: PROC01 | Downstream: PROC14, PROC24, PROC25.
Comments: Strongly interacts with continuous material flow capacities | #des #config ##tank-farm ##storage

PROC04 Utility System & Cogeneration Synthesis 
Description: Selects the discrete configuration of boilers, turbines, and heat exchangers for plant-wide utility generation.
Template: Superstructure optimization / network design | MINLP, MIP.
Relevance: Priority: High | Energy costs represent a massive fraction of operating expenditure.
Hardness: Class: NP-hard | Discrete existence of units combined with non-linear thermodynamics.
Dependencies: Upstream: PROC02 | Downstream: PROC13.
Comments: Focus is on structural choice, not continuous load balancing | #des #config ##utilities ##energy

PROC05 Recipe-Structure Configuration 
Description: Defines standard production recipes by selecting unit procedures, equipment classes, and material balances for product variants.
Template: Recipe assignment / compatibility selection | CP-SAT, MIP.
Relevance: Priority: High | Core in batch pharma and food manufacturing for scalability, flexibility, and regulatory compliance.
Hardness: Class: NP-hard | Assignment with alternative routings generalizes the set-cover problem.
Dependencies: Upstream: PROC02 | Downstream: PROC07, PROC10, PROC16.
Comments: Establishes ISA-88 compliant master recipes | #des #config ##recipes ##ISA88

2) PLANNING

PROC06 Multi-Site Process Allocation 
Description: Allocates production of bulk product families across a global network of process plants.
Template: Multi-period generalized assignment / network flow | MIP.
Relevance: Priority: High | Balances global demand, raw material proximity, and plant capacities.
Hardness: Class: NP-hard | Generalizes the capacitated facility location and assignment problems.
Dependencies: Upstream: PROC01 | Downstream: PROC07, PROC09.
Comments: Highest level of structural supply chain planning | #plan #alloc ##multi-site ##supply-chain

PROC07 Multi-Product Production Planning 
Description: Allocates production quantities across products and time periods under capacity, inventory, and demand constraints.
Template: Multi-period multi-commodity planning | MIP, rolling-horizon.
Relevance: Priority: Critical | Aggregates market demand into campaign intent in continuous plants.
Hardness: Class: NP-hard | Capacitated multi-item planning is strongly NP-hard.
Dependencies: Upstream: PROC05, PROC06 | Downstream: PROC08, PROC10.
Comments: Links sales forecasts to plant-level feasibility | #plan #select ##production-planning

PROC08 Campaign Planning 
Description: Groups products into long-to-medium term campaigns (sequences of product lots) to minimize major structural changeovers and cleanings over the horizon.
Template: Sequence-dependent clustering / lot-sizing | MIP, heuristic clustering, decomposition.
Relevance: Priority: Critical | Standard in food, pharma, and bioprocesses for managing multi-product plants efficiently.
Hardness: Class: NP-hard | Campaign sequencing embeds TSP-like problems within lot sizing.
Dependencies: Upstream: PROC07 | Downstream: PROC11, PROC19, PROC20.
Comments: Bridging decision between annual planning and weekly scheduling | #plan #select ##campaigns ##multi-product

PROC09 Raw Material Procurement & Blending Planning 
Description: Selects supplier lots and defines macroscopic blends to meet recipe specifications and inventory targets under quality constraints.
Template: Multi-blend knapsack + assignment / pooling problem | MINLP, MIP.
Relevance: Priority: High | Critical in refining and polymers for feedstock optimization and cost reduction.
Hardness: Class: NP-hard | Blend selection generalizes knapsack; pooling introduces bilinear non-convexities.
Dependencies: Upstream: PROC06 | Downstream: PROC14, PROC24.
Comments: Quality-constrained procurement | #plan #alloc ##blending ##feedstock

PROC10 Process Lot Sizing & Run Length Planning 
Description: Determines the discrete lengths and quantities of continuous production runs or the exact number of batches per product.
Template: Capacitated lot-sizing problem (CLSP) | MIP, Dynamic Programming.
Relevance: Priority: Critical | Balances inventory holding costs against massive process changeover losses.
Hardness: Class: NP-hard | CLSP with setups is strictly NP-hard.
Dependencies: Upstream: PROC05, PROC07 | Downstream: PROC14, PROC18.
Comments: Defines the primary discrete targets for plant-floor execution | #plan #select ##lot-sizing ##run-length

3) RESOURCE ALLOCATION

PROC11 Turnaround & Maintenance Campaign Scheduling 
Description: Plans shutdown scopes and timings across units to balance equipment reliability with production loss and contractor availability.
Template: Multi-resource project scheduling (RCPSP) | MIP, CP-SAT.
Relevance: Priority: Critical | Major downtime driver in continuous plants, costing millions per day.
Hardness: Class: NP-hard | Generalization of the Resource-Constrained Project Scheduling Problem.
Dependencies: Upstream: PROC08 | Downstream: PROC15, PROC18, PROC20.
Comments: Often sets the rigid macro-calendar for the entire plant | #alloc #calendars ##maintenance ##shutdown

PROC12 Operator Task & Shift Assignment 
Description: Assigns certified operators and safety crews to process units and continuous 24/7 shifts under skill, coverage, and regulatory constraints.
Template: Skill-constrained rostering / set covering | MIP, CP-SAT, column generation.
Relevance: Priority: High | Safety-critical in staffed chemical and pharmaceutical plants.
Hardness: Class: NP-hard | Highly constrained generalization of nurse rostering.
Dependencies: Upstream: PROC07 | Downstream: PROC18, PROC20.
Comments: The human safety and operational availability envelope | #alloc #skills ##operators ##rostering

PROC13 Utility & Energy Unit Commitment 
Description: Schedules the discrete on/off states of auxiliary utility generators (boilers, chillers) to support scheduled production peaks.
Template: Unit commitment problem / resource allocation | MIP.
Relevance: Priority: High | Binding in energy-intensive refining and chemical facilities.
Hardness: Class: NP-hard | Knapsack-like problem with complex ramp-up and min-uptime constraints.
Dependencies: Upstream: PROC04, PROC10 | Downstream: PROC17, PROC18.
Comments: Ensures thermodynamic utilities are available without massive waste | #alloc #sched ##utilities ##unit-commitment

PROC14 Tank Allocation & Inventory Segregation 
Description: Assigns specific intermediate materials or final products to specific discrete storage tanks to prevent cross-contamination.
Template: Dynamic assignment / coloring problem | MIP, CP-SAT.
Relevance: Priority: High | Erroneous mixing destroys product value; flexible tanks are strictly limited.
Hardness: Class: NP-hard | Generalizes dynamic bin-packing and assignment problems.
Dependencies: Upstream: PROC03, PROC09, PROC10 | Downstream: PROC22, PROC24.
Comments: Creates the state-space limits for physical material flow | #alloc #flow ##tank-assignment ##inventory

PROC15 Unit Cleaning & Availability Calendars 
Description: Schedules mandated cleaning and sanitization windows for units to manage contamination risks and preserve product hygiene.
Template: Calendar-constrained scheduling | MIP, CP-SAT.
Relevance: Priority: High | Essential for product purity and FDA compliance in pharma/food.
Hardness: Class: NP-hard | Preemptive scheduling with strict availability windows.
Dependencies: Upstream: PROC11 | Downstream: PROC18, PROC21.
Comments: Distinct from active CIP routing; this sets the hygiene calendar bounds | #alloc #calendars ##cleaning ##availability

4) OPERATIONS

PROC16 Recipe-Unit Assignment 
Description: Assigns executable recipes (products) to specific processing units or trains considering compatibility, certification, and capacity.
Template: Generalized assignment with side-constraints | MIP, CP-SAT.
Relevance: Priority: High | Crucial for multi-product and multi-train allocation before detailed sequencing.
Hardness: Class: NP-hard | Assignment problem with complex compatibility matrices.
Dependencies: Upstream: PROC05, PROC10, PROC15 | Downstream: PROC17, PROC18.
Comments: The primary product-to-train matching step | #ops #alloc ##assignment ##multi-mode

PROC17 State-Task / Resource-Task Network (STN/RTN) Scheduling 
Description: Unifies the assignment and sequencing of chemical/physical tasks to generic equipment units over time with rigorous mass balances.
Template: Network-based batch scheduling (STN/RTN) | MIP (discrete or continuous time).
Relevance: Priority: Critical | The foundational paradigm for mathematical chemical process scheduling.
Hardness: Class: NP-hard | Integrates assignment, sequencing, and continuous inventory mass balances simultaneously.
Dependencies: Upstream: PROC13, PROC16 | Downstream: PROC18, PROC22.
Comments: Represents the core complexity of process OR literature | #ops #sched ##STN ##RTN ##batch

PROC18 Multi-Purpose Batch Plant Scheduling 
Description: Sequences a portfolio of discrete batch recipes across highly flexible, interconnected equipment networks.
Template: Flexible job-shop with complex batching/splitting | MIP, CP-SAT.

Relevance: Priority: Critical | Standard in active pharmaceutical ingredients (API) and specialty chemical manufacturing.
Hardness: Class: NP-hard | Job-shop generalization complicated by material splitting, mixing, and recycling.
Dependencies: Upstream: PROC10, PROC11, PROC12, PROC15, PROC17 | Downstream: PROC21, PROC22.
Comments: The process-manufacturing equivalent of the flexible job shop | #ops #sched ##multi-purpose ##batch-plant

PROC19 Sequence-Dependent Transition & Grade-Change Sequencing 
Description: Sequences production campaigns on continuous lines to minimize the off-spec material, cost, and time of transitioning between product grades (e.g., color, viscosity).
Template: Asymmetric TSP with setups / intermediate states | MIP, CP-SAT, LNS.
Relevance: Priority: Critical | Dominant cost factor in polymers, paper, and food grade changes.
Hardness: Class: NP-hard | Equivalent to ATSP with complex transition loss functions.
Dependencies: Upstream: PROC08, PROC16 | Downstream: PROC22, PROC25.
Comments: Minimizes the generation of transition scrap | #ops #sched ##transitions ##grade-change

PROC20 Parallel Train Scheduling & Load Balancing 
Description: Schedules and sequences campaigns across parallel identical or unrelated processing trains.
Template: Parallel machine batch scheduling | CP-SAT, MIP.
Relevance: Priority: Critical | Standard operational problem in refining and multi-train chemical facilities.
Hardness: Class: NP-hard | P||Cmax generalization with process constraints.
Dependencies: Upstream: PROC08, PROC11, PROC12 | Downstream: PROC19, PROC22.
Comments: Balances load and coordinates throughput across site capacity | #ops #sched ##parallel-trains

PROC21 Clean-in-Place (CIP) Routing & Scheduling 
Description: Schedules shared mobile or stationary cleaning units to wash tanks and pipes between incompatible batches.
Template: Resource-constrained scheduling with blocking | MIP, CP-SAT.
Relevance: Priority: Critical | Mandatory in food, beverage, and pharma to prevent catastrophic contamination.
Hardness: Class: NP-hard | CIP systems act as heavily constrained, shared mobile resources that frequently bottleneck plants.
Dependencies: Upstream: PROC15, PROC18 | Downstream: PROC22.
Comments: Often the hidden bottleneck severely restricting batch throughput | #ops #sched ##CIP ##cleaning

PROC22 Material Transfer & Piping Synchronization 
Description: Schedules the physical transfer of fluids between units, avoiding pipe collisions, header contention, and pump limits.
Template: Resource-constrained flow scheduling | MIP, CP-SAT.
Relevance: Priority: High | Complex topologies prevent arbitrary simultaneous transfers.
Hardness: Class: NP-hard | Adds routing and synchronization constraints on top of task scheduling.
Dependencies: Upstream: PROC14, PROC17, PROC18, PROC19, PROC20, PROC21 | Downstream: PROC23, PROC24.
Comments: Bridges mathematical schedules with physical pipe and valve reality | #ops #flow ##transfer ##synchronization

PROC23 Restricted Wait-Time Batch Scheduling (ZW/NIS/FIS) 
Description: Schedules operations under strict storage policies like Zero-Wait (ZW), No Intermediate Storage (NIS), or Finite Intermediate Storage (FIS).
Template: Blocking and no-wait scheduling | CP-SAT, MIP.
Relevance: Priority: High | Unstable chemical intermediates or hot materials cannot sit in holding tanks.
Hardness: Class: NP-hard | No-wait constraints severely restrict the feasible schedule space, often making finding even a feasible solution hard.
Dependencies: Upstream: PROC18, PROC22 | Downstream: PROC25.
Comments: Chemical necessity dictates rigid mathematical blocking constraints | #ops #sched ##zero-wait ##blocking

PROC24 Short-Term Blending & Transfer Scheduling 
Description: Decides the short-term sequencing of blends from intermediate tanks into final product headers or loading bays.
Template: Continuous-time blending scheduling | MINLP, MIP.
Relevance: Priority: High | The final execution step in refineries and bulk liquids.
Hardness: Class: NP-hard | Highly combinatorial sequencing combined with non-linear blend rules.
Dependencies: Upstream: PROC09, PROC14, PROC22 | Downstream: PROC25.
Comments: Operates on extremely tight time horizons (hours to days) | #ops #sched ##blending

PROC25 Bulk-to-Packaging Synchronization 
Description: Synchronizes continuous or large-batch bulk production with downstream discrete high-speed packaging lines.
Template: Hybrid continuous-discrete scheduling | MIP, CP-SAT.
Relevance: Priority: High | Universal bottleneck in fast-moving consumer goods (FMCG), food, and beverage sectors.
Hardness: Class: NP-hard | Mismatched production rates and complex buffers make this intractable at scale.
Dependencies: Upstream: PROC19, PROC23, PROC24 | Downstream: —.
Comments: The ultimate physical interface between PROC (process) and PROD (discrete) environments | #ops #flow ##packaging ##synchronization

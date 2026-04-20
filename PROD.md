PROD  (Discrete Manufacturing Systems)
========================================================

Scope:
Discrete manufacturing systems including job shops, flow lines, assembly lines,
flexible manufacturing systems (FMS), and mixed‑model production.
Continuous/process manufacturing is explicitly excluded (handled under PROC).


--------------------------------------------------------
1) DESIGN / STRUCTURAL CONFIGURATION
--------------------------------------------------------

PROD01 Assembly Line Balancing (SALBP)
Description: Assigns tasks to stations under precedence, cycle‑time, and station‑capacity constraints.
Template Problem: Simple / generalized assembly‑line balancing (SALBP, ALWABP) | MIP, CP‑SAT, branch‑and‑bound, heuristic bin‑packing.
Relevance: Priority: Critical | Found in nearly all assembly lines.
Hardness: Class: NP‑hard | Line‑balancing is a classic NP‑hard assignment problem.
Dependencies: Upstream: — | Downstream: PROD25, PROD22, PROD14.
Comments: Defines the physical workload structure of an assembly line | #des #config ##line‑balancing ##assembly


PROD02 Tool Loading & Magazine Management
Description: Allocates tools to machine magazines under capacity and job‑compatibility constraints.
Template Problem: Multiple knapsack / set‑covering tool‑loading | MIP, CP‑SAT, heuristic loading.
Relevance: Priority: High | Central complexity source in FMS and CNC‑rich plants.
Hardness: Class: NP‑hard | Tool loading generalizes knapsack and set‑cover problems.
Dependencies: Upstream: — | Downstream: PROD06, PROD18, PROD19, PROD20.
Comments: Determines feasibility of downstream shop schedules | #des #alloc ##tool‑management ##FMS


PROD03 Fixture Allocation & Clamping
Description: Assigns fixtures and clamping devices to machines under geometric and capacity constraints.
Template Problem: Assignment / geometric packing with side constraints | MIP, CP‑SAT, packing heuristics.
Relevance: Priority: Medium | Important in machining and reconfigurable cells.
Hardness: Class: NP‑hard | Packing and assignment with constraints is combinatorial.
Dependencies: Upstream: — | Downstream: PROD15, PROD19, PROD20.
Comments: Often implicit but binding feasibility constraint | #des #alloc ##fixtures ##clamping


PROD04 Palletization & Part‑Family Grouping
Description: Groups parts into pallets or families for efficient machine loading and transport.
Template Problem: Clustering + bin‑packing | MIP, CP‑SAT, heuristics.
Relevance: Priority: Medium | Common in robotic cells and FMS.
Hardness: Class: NP‑hard | Clustering plus packing is NP‑hard.
Dependencies: Upstream: — | Downstream: PROD26, PROD27.
Comments: Shapes internal material flow topology | #des #config ##palletization ##part‑families


PROD05 Buffer Sizing & Placement
Description: Chooses buffer locations and capacities to balance throughput, blocking, and WIP.
Template Problem: Facility / network design under capacity trade‑offs | MIP, simulation‑optimization.
Relevance: Priority: Medium | Strong effect on throughput and stability.
Hardness: Class: NP‑hard | Buffer design generalizes knapsack/design problems.
Dependencies: Upstream: — | Downstream: PROD27, PROD24.
Comments: Structural decoupling mechanism | #des #invest ##buffers ##throughput


PROD06 Tool Assignment + Sequencing (Joint)
Description: Jointly assigns tools to machines and sequences jobs to minimize tool changes and makespan.
Template Problem: Joint assignment–sequencing problem | CP‑SAT, MIP, decomposition, large‑neighborhood search.
Relevance: Priority: High | Core combinatorial bottleneck in CNC cells.
Hardness: Class: NP‑hard | Joint decisions amplify hardness.
Dependencies: Upstream: PROD02 | Downstream: PROD15, PROD19, PROD20.
Comments: Design–operation coupling problem | #des #sched ##tool‑assignment ##joint‑decision


--------------------------------------------------------
2) PLANNING (Demand, Material, Release Intent)
--------------------------------------------------------

PROD07 Capacitated Order Acceptance & Planning
Description: Selects which customer orders to accept and when to serve them under capacity and margin constraints.
Template Problem: Knapsack / subset‑selection with multi‑period planning | MIP, CP‑SAT.
Relevance: Priority: Medium | Used when demand exceeds capacity.
Hardness: Class: NP‑hard | Order selection generalizes knapsack.
Dependencies: Upstream: — | Downstream: PROD08, PROD09.
Comments: Entry point of demand into production | #plan #select ##order‑acceptance


PROD08 Multi‑Level Production Planning (MLPP)
Description: Plans multi‑item, multi‑level production across BOMs, inventories, and capacities over time.
Template Problem: Multi‑stage capacity‑constrained planning | MIP, CP‑SAT, rolling‑horizon, MRP heuristics.
Relevance: Priority: Critical | Integrates demand with plant‑wide feasibility.
Hardness: Class: NP‑hard | Multi‑period, multi‑level planning is NP‑hard.
Dependencies: Upstream: PROD07 | Downstream: PROD11.
Comments: Translates demand into feasible production intent | #plan #select ##MLPP


PROD09 Master Production Scheduling (MPS)
Description: Defines release quantities and timings across products and families.
Template Problem: Discrete multi‑period integer planning | MIP, CP‑SAT, rolling‑horizon.
Relevance: Priority: Critical | Primary interface between planning and shop scheduling.
Hardness: Class: NP‑hard | Integer release planning is NP‑hard.
Dependencies: Upstream: PROD07 | Downstream: PROD10, PROD11.
Comments: Controls execution release | #plan #select ##MPS


PROD10 BOM Explosion with Alternatives & Substitutes
Description: Expands MPS through BOMs with alternative routings, variants, and substitutes.
Template Problem: Network flow with discrete routing choices | MIP, CP‑SAT.
Relevance: Priority: High | Common in configurable manufacturing.
Hardness: Class: NP‑hard | Alternative routing induces combinatorial branching.
Dependencies: Upstream: PROD09 | Downstream: PROD11.
Comments: Materializes structural feasibility | #plan #flow ##BOM ##alternatives


PROD11 Lot Sizing (Capacitated)
Description: Determines lot sizes and timing subject to setup costs and capacity limits.
Template Problem: Capacitated lot‑sizing (CLSP) | MIP, dynamic programming, fix‑and‑optimize.
Relevance: Priority: Critical | Drives setups, inventory, and utilization.
Hardness: Class: NP‑hard | Capacitated lot sizing is NP‑hard.
Dependencies: Upstream: PROD08, PROD09, PROD10 | Downstream: PROD15, PROD16, PROD19, PROD22.
Comments: Links planning horizon to shop execution | #plan #select ##lot‑sizing


--------------------------------------------------------
3) RESOURCE AVAILABILITY / CALENDARS
--------------------------------------------------------

PROD12 Operator and Crew Scheduling
Description: Assigns workers to machines and cells under skill and coverage constraints.
Template Problem: Crew scheduling with skills | MIP, CP‑SAT.
Relevance: Priority: High | Labor is often binding.
Hardness: Class: NP‑hard | Skill‑constrained crew scheduling is NP‑hard.
Dependencies: Upstream: PROD08, PROD09 | Downstream: PROD15, PROD19, PROD25.
Comments: Human availability envelope | #plan #alloc ##workforce ##skills


PROD13 Shift Scheduling for Production
Description: Builds rosters for production and support staff.
Template Problem: Workforce rostering | CP‑SAT, column generation.
Relevance: Priority: High | Universal in staffed plants.
Hardness: Class: NP‑hard | Rostering is NP‑hard.
Dependencies: Upstream: PROD12 | Downstream: PROD15, PROD19, PROD25.
Comments: Temporal labor feasibility | #plan #alloc ##shifts


PROD14 Maintenance‑Integrated Scheduling
Description: Integrates planned maintenance windows into production schedules.
Template Problem: Scheduling with machine availability calendars | CP‑SAT, MIP.
Relevance: Priority: High | Reflects real plant constraints.
Hardness: Class: NP‑hard | Calendar constraints add hardness.
Dependencies: Upstream: PROD08, PROD09 | Downstream: PROD15, PROD16, PROD17, PROD18, PROD19, PROD20.
Comments: Availability overlay constraint | #plan #sched ##maintenance


--------------------------------------------------------
4) OPERATIONS (Scheduling, Sequencing, Flow)
--------------------------------------------------------

PROD15 Single‑Machine Sequencing
Description: Schedules jobs on one machine with release dates, due dates, and setups.
Template Problem: 1|r_j,s_ij|∑w_jT_j | CP‑SAT, MIP.
Relevance: Priority: Critical | Nearly every plant has bottlenecks.
Hardness: Class: NP‑hard | Sequencing with setups is NP‑hard.
Dependencies: Upstream: PROD08, PROD09, PROD11, PROD12, PROD13, PROD14, PROD06 | Downstream: PROD22, PROD24, PROD27.
Comments: Execution bottleneck kernel | #ops #sched ##single‑machine


PROD16 Parallel Machine Scheduling
Description: Assigns and sequences jobs over identical or unrelated machines.
Template Problem: P_m / Q_m / R_m scheduling | CP‑SAT, MIP.
Relevance: Priority: Critical | Ubiquitous in machining centers.
Hardness: Class: NP‑hard | Most variants are NP‑hard.
Dependencies: Upstream: PROD08, PROD09, PROD12, PROD14 | Downstream: PROD18, PROD27.
Comments: Capacity loading across machines | #ops #sched ##parallel‑machines


PROD17 Flow Shop Scheduling (FSS)
Description: Schedules jobs through a fixed sequence of stages.
Template Problem: Permutation / non‑permutation flow shop | CP‑SAT, heuristics.
Relevance: Priority: High | Common in staged lines.
Hardness: Class: NP‑hard.
Dependencies: Upstream: PROD08, PROD09 | Downstream: PROD18, PROD24.
Comments: Structured shop abstraction | #ops #sched ##flow‑shop


PROD18 Hybrid Flow Shop (HFS)
Description: Schedules jobs through stages with parallel machines.
Template Problem: Hybrid flow shop | CP‑SAT, MIP.
Relevance: Priority: High | Assembly and finishing lines.
Hardness: Class: NP‑hard.
Dependencies: Upstream: PROD08, PROD09, PROD14 | Downstream: PROD17, PROD19, PROD27.
Comments: Partial flexibility model | #ops #sched ##hybrid‑flow‑shop


PROD19 Job Shop Scheduling (JSS)
Description: Orders job operations across machines under precedence constraints.
Template Problem: Disjunctive JSS | CP‑SAT, MIP.
Relevance: Priority: Critical | Canonical discrete manufacturing model.
Hardness: Class: NP‑hard.
Dependencies: Upstream: PROD08, PROD09, PROD02, PROD03, PROD06, PROD14 | Downstream: PROD27, PROD23.
Comments: Flexible routing kernel | #ops #sched ##job‑shop


PROD20 Flexible Job Shop Scheduling (FJSS)
Description: Extends JSS by permitting alternative machines per operation.
Template Problem: FJSS | CP‑SAT, decomposition.
Relevance: Priority: Critical | Matches CNC cells.
Hardness: Class: NP‑hard.
Dependencies: Upstream: PROD08, PROD09, PROD02, PROD03, PROD06, PROD14 | Downstream: PROD27, PROD23.
Comments: Assign‑then‑sequence coupling | #ops #sched ##flexible‑job‑shop


PROD21 Open Shop Scheduling
Description: Schedules jobs whose operations have no fixed order.
Template Problem: Open‑shop scheduling | CP‑SAT.
Relevance: Priority: Medium.
Hardness: Class: NP‑hard.
Dependencies: Upstream: PROD08, PROD09 | Downstream: PROD27.
Comments: Maximum routing freedom | #ops #sched ##open‑shop


PROD22 Sequence‑Dependent Changeover Sequencing
Description: Sequences jobs to minimize setup or color change penalties.
Template Problem: TSP‑like sequencing | CP‑SAT, MIP.
Relevance: Priority: High.
Hardness: Class: NP‑hard.
Dependencies: Upstream: PROD11, PROD15, PROD17 | Downstream: PROD19, PROD20, PROD27.
Comments: Major efficiency driver | #ops #sched ##changeovers


PROD23 Batch Scheduling & Sequencing
Description: Forms and sequences batches of compatible jobs.
Template Problem: Batch formation plus sequencing | CP‑SAT.
Relevance: Priority: High.
Hardness: Class: NP‑hard.
Dependencies: Upstream: PROD11, PROD19, PROD20 | Downstream: PROD27.
Comments: Packing–sequencing interaction | #ops #sched ##batching


PROD24 Lot Streaming & Sublot Scheduling
Description: Splits lots into sublots to reduce flow time.
Template Problem: Sublot scheduling | CP‑SAT.
Relevance: Priority: Medium.
Hardness: Class: NP‑hard.
Dependencies: Upstream: PROD11, PROD15, PROD17 | Downstream: PROD27.
Comments: Throughput accelerator | #ops #sched ##lot‑streaming


PROD25 Mixed‑Model Assembly Sequencing
Description: Sequences product variants on a mixed‑model assembly line.
Template Problem: Smoothing‑constrained sequencing | CP‑SAT, MIP.
Relevance: Priority: High.
Hardness: Class: NP‑hard.
Dependencies: Upstream: PROD01, PROD09, PROD12, PROD13 | Downstream: PROD27.
Comments: Variability smoothing | #ops #sched ##mixed‑model


PROD26 AGV / Internal Transport Routing
Description: Routes AGVs and internal transport under conflicts and timing constraints.
Template Problem: Vehicle routing with conflicts | CP‑SAT, MIP.
Relevance: Priority: High.
Hardness: Class: NP‑hard.
Dependencies: Upstream: PROD04 | Downstream: PROD27.
Comments: Physical flow backbone | #ops #route ##AGV


PROD27 Material Handling Synchronization
Description: Synchronizes machines, buffers, and transport to avoid blocking and starvation.
Template Problem: Resource‑constrained scheduling / blocking models | CP‑SAT.
Relevance: Priority: High.
Hardness: Class: NP‑hard.
Dependencies: Upstream: PROD05, PROD15–PROD26 | Downstream: PROD15–PROD21.
Comments: Where schedules meet physics | #ops #flow ##material‑handling

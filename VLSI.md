**VLSI (Design and Production Systems)**  
========================================================  

**Scope:**  
VLSI design (RTL to GDSII physical layout/timing) and wafer fabrication production (re-entrant flow, mask/yield optimization). Focus on combinatorial decisions; exclude circuit simulation, analog sizing, or purely continuous convex flows. [or.uni-bonn](http://www.or.uni-bonn.de/~vygen/files/buda.pdf)

--------------------------------------------------------  
**1) DESIGN / STRUCTURAL CONFIGURATION**  
--------------------------------------------------------  

**VLSI01 Circuit Partitioning**  
**Description:** Divides netlist into balanced sub-circuits minimizing cut-edges for hierarchical layout or multi-chip modules. [linkedin](https://www.linkedin.com/posts/sai-manikanta-6022981a3_complexity-issues-and-np-hard-problems-in-activity-7309128000850014208-bDtU)
**Template:** Graph partitioning (min-cut, balanced) | FM heuristic, spectral, multilevel.  
**Relevance:** Priority: Critical | Foundation for floorplanning, placement, FPGA partitioning. [linkedin](https://www.linkedin.com/posts/sai-manikanta-6022981a3_complexity-issues-and-np-hard-problems-in-activity-7309128000850014208-bDtU)  
**Hardness:** Class: NP-hard | Min-balanced-cut NP-hard. [linkedin](https://www.linkedin.com/posts/sai-manikanta-6022981a3_complexity-issues-and-np-hard-problems-in-activity-7309128000850014208-bDtU)  
**Dependencies:** Upstream: — | Downstream: VLSI04, VLSI05.  
**Comments:** Enables hierarchical design | #des #config ##partitioning ##hypergraph  

**VLSI02 Floorplanning**  
**Description:** Arranges functional blocks/modules topologically minimizing area, wirelength, and congestion. [research.utwente](https://research.utwente.nl/en/publications/complexity-and-approximability-results-for-slicing-floorplan-desi)
**Template:** Slicing/non-slicing floorplan optimization | Sequence-pair, BSG, simulated annealing.  
**Relevance:** Priority: Critical | High-level layout defining chip topology. [research.utwente](https://research.utwente.nl/en/publications/complexity-and-approximability-results-for-slicing-floorplan-desi)  
**Hardness:** Class: NP-hard | Floorplan area minimization NP-hard. [research.utwente](https://research.utwente.nl/en/publications/complexity-and-approximability-results-for-slicing-floorplan-desi)  
**Dependencies:** Upstream: VLSI01 | Downstream: VLSI04, VLSI05.  
**Comments:** Topological block placement | #des #config ##floorplan ##slicing  

**VLSI03 Clock Tree Synthesis**  
**Description:** Builds buffered clock distribution network minimizing skew, slew, and power under topology constraints. [or.uni-bonn](http://www.or.uni-bonn.de/~vygen/files/buda.pdf)
**Template:** Steiner tree + buffer insertion | DME, CTS tools (e.g., Synopsys ICC).  
**Relevance:** Priority: Critical | Ensures timing closure in synchronous designs. [linkedin](https://www.linkedin.com/posts/sai-manikanta-6022981a3_complexity-issues-and-np-hard-problems-in-activity-7309128000850014208-bDtU)  
**Hardness:** Class: NP-hard | Bounded-skew CTS NP-hard.  
**Dependencies:** Upstream: VLSI04 | Downstream: VLSI09.  
**Comments:** H-tree/variant topologies | #des #config ##clock-tree ##skew  

--------------------------------------------------------  
**2) PLANNING (Demand, Material, Release Intent)**  
--------------------------------------------------------  

**VLSI04 Technology Mapping & Logic Synthesis**  
**Description:** Selects gate implementations and library cells for netlist minimizing area/delay under timing constraints. [or.uni-bonn](http://www.or.uni-bonn.de/~vygen/files/buda.pdf)
**Template:** Tree covering + DAG mapping | DAGON, LSOracle, algebraic methods.  
**Relevance:** Priority: Critical | Translates RTL to gate-level for physical design. [or.uni-bonn](http://www.or.uni-bonn.de/~vygen/files/buda.pdf)  
**Hardness:** Class: NP-hard | Exact mapping NP-hard.  
**Dependencies:** Upstream: VLSI01 | Downstream: VLSI05, VLSI06.  
**Comments:** Library-aware synthesis | #plan #select ##tech-mapping ##synthesis  

**VLSI05 Retiming & Logic Restructuring**  
**Description:** Repositions registers and restructures logic to optimize cycle time/pipeline balance. [or.uni-bonn](https://www.or.uni-bonn.de/research/montreal.pdf)
**Template:** Graph transformation + retiming | Min-area retiming, ILP.  
**Relevance:** Priority: High | Critical for timing optimization pre-placement.  
**Hardness:** Class: NP-hard | Min-register retiming NP-hard.  
**Dependencies:** Upstream: VLSI04 | Downstream: VLSI03, VLSI07.  
**Comments:** Sequential optimization | #plan #flow ##retiming ##pipelining  

**VLSI06 Mask Set Planning**  
**Description:** Plans multi-layer mask volumes and priorities for wafer production runs. [citeseerx.ist.psu](https://citeseerx.ist.psu.edu/document?repid=rep1&type=pdf&doi=547bb29849c5a5e68901c29e97383fa54bb20f42)
**Template:** Multi-resource lot planning | MIP, heuristics.  
**Relevance:** Priority: Medium | Costly in production ramp-up.  
**Hardness:** Class: NP-hard | Multi-period planning NP-hard.  
**Dependencies:** Upstream: — | Downstream: VLSI14, VLSI15.  
**Comments:** Lithography cost driver | #plan #select ##masks ##production  

--------------------------------------------------------  
**3) RESOURCE ALLOCATION (Calendars, Matching, Assignment)**  
--------------------------------------------------------  

**VLSI07 Standard Cell Placement**  
**Description:** Assigns/positions cells in rows minimizing wirelength, density, congestion. [linkedin](https://www.linkedin.com/posts/sai-manikanta-6022981a3_complexity-issues-and-np-hard-problems-in-activity-7309128000850014208-bDtU)
**Template:** Quadratic + force-directed placement | Analytical (e.g., NTUplace), simulated annealing.  
**Relevance:** Priority: Critical | Core physical design step. [linkedin](https://www.linkedin.com/posts/sai-manikanta-6022981a3_complexity-issues-and-np-hard-problems-in-activity-7309128000850014208-bDtU)  
**Hardness:** Class: NP-hard | Min-wirelength placement NP-hard. [linkedin](https://www.linkedin.com/posts/sai-manikanta-6022981a3_complexity-issues-and-np-hard-problems-in-activity-7309128000850014208-bDtU)  
**Dependencies:** Upstream: VLSI02, VLSI04 | Downstream: VLSI08, VLSI09.  
**Comments:** Global/detailed phases | #alloc ##placement ##wirelength  

**VLSI08 Operator/Task Assignment (Fab)**  
**Description:** Assigns technicians to tools/wafer lots under skill/certification constraints. [sciencedirect](https://www.sciencedirect.com/science/article/abs/pii/S0360835216300821)
**Template:** Skill-constrained rostering | MIP, CP-SAT.  
**Relevance:** Priority: High | Labor binding in cleanroom fabs.  
**Hardness:** Class: NP-hard | Assignment NP-hard.  
**Dependencies:** Upstream: VLSI06 | Downstream: VLSI15.  
**Comments:** Human fab resources | #alloc #skills ##operators ##fab  

**VLSI09 Maintenance & Tool Availability**  
**Description:** Schedules preventive maintenance on tools minimizing downtime impact. [sciencedirect](https://www.sciencedirect.com/science/article/abs/pii/S0360835216300821)
**Template:** Calendar-constrained scheduling | RCPSP, MIP.  
**Relevance:** Priority: High | Tool uptime critical for yield.  
**Hardness:** Class: NP-hard | RCPSP NP-hard.  
**Dependencies:** Upstream: VLSI06 | Downstream: VLSI15.  
**Comments:** PM windows in re-entrant flow | #alloc #calendars ##maintenance ##tools  

--------------------------------------------------------  
**4) OPERATIONS (Scheduling, Sequencing, Flow)**  
--------------------------------------------------------  

**VLSI10 Global Routing**  
**Description:** Routes nets through channels/grids minimizing congestion and wirelength. [linkedin](https://www.linkedin.com/posts/sai-manikanta-6022981a3_complexity-issues-and-np-hard-problems-in-activity-7309128000850014208-bDtU)
**Template:** Multi-commodity flow + Steiner trees | Negotiated congestion, maze routing.  
**Relevance:** Priority: Critical | Pre-detailed routing feasibility. [linkedin](https://www.linkedin.com/posts/sai-manikanta-6022981a3_complexity-issues-and-np-hard-problems-in-activity-7309128000850014208-bDtU)  
**Hardness:** Class: NP-hard | Steiner tree/routing NP-hard. [or.uni-bonn](http://www.or.uni-bonn.de/~vygen/files/buda.pdf)  
**Dependencies:** Upstream: VLSI07 | Downstream: VLSI11.  
**Comments:** Capacity-constrained paths | #ops #route ##global-routing ##congestion  

**VLSI11 Detailed Routing**  
**Description:** Completes point-to-point wire paths avoiding vias/detours under design rules. [or.uni-bonn](http://www.or.uni-bonn.de/~vygen/files/buda.pdf)
**Template:** Maze/rectilinear Steiner + DRC | Greedy, rip-up retry.  
**Relevance:** Priority: Critical | Signoff routing closure. [linkedin](https://www.linkedin.com/posts/sai-manikanta-6022981a3_complexity-issues-and-np-hard-problems-in-activity-7309128000850014208-bDtU)  
**Hardness:** Class: NP-hard | Exact routing NP-hard.  
**Dependencies:** Upstream: VLSI07, VLSI10 | Downstream: VLSI12.  
**Comments:** DRC/layer assignment | #ops #route ##detailed-routing ##DRC  

**VLSI12 Wafer Lot Release & Re-entrant Scheduling**  
**Description:** Releases wafer lots to 100s of steps/tools minimizing cycle time/WIP. [tandfonline](https://www.tandfonline.com/doi/abs/10.1080/00207543.2025.2584726)
**Template:** Re-entrant flow scheduling (e.g., SWFS) | Dispatching rules, MILP, RL. [sciencedirect](https://www.sciencedirect.com/science/article/abs/pii/S0360835216300821)  
**Relevance:** Priority: Critical | Fab throughput bottleneck. [tandfonline](https://www.tandfonline.com/doi/abs/10.1080/00207543.2025.2584726)  
**Hardness:** Class: NP-hard | WLSP strongly NP-hard. [tandfonline](https://www.tandfonline.com/doi/abs/10.1080/00207543.2025.2584726)  
**Dependencies:** Upstream: VLSI06 | Downstream: VLSI15.  
**Comments:** 300+ step loops | #ops #sched ##wafer-scheduling ##re-entrant  

**VLSI13 Sequence-Dependent Setup Sequencing**  
**Description:** Sequences lots on tools minimizing recipe/device changeovers. [sciencedirect](https://www.sciencedirect.com/science/article/abs/pii/S0278612521001801)
**Template:** TSP with setups | LNS, CP-SAT.  
**Relevance:** Priority: High | Setup time dominant in fab tools.  
**Hardness:** Class: NP-hard | Sequencing NP-hard.  
**Dependencies:** Upstream: VLSI12 | Downstream: VLSI15.  
**Comments:** Clean/drydock changeovers | #ops #sched ##setups ##recipe  

**VLSI14 Yield-Aware Test Pattern Sequencing**  
**Description:** Sequences scan chains/ATPG patterns minimizing defect escape under time constraints. [dl.acm](https://dl.acm.org/doi/abs/10.5555/1354644)
**Template:** Ordering + compression | MIP, heuristics.  
**Relevance:** Priority: Medium | Post-fab quality gate.  
**Hardness:** Class: NP-hard | Pattern selection NP-hard.  
**Dependencies:** Upstream: VLSI11 | Downstream: —.  
**Comments:** ATPG optimization | #ops #test ##yield ##scan  

**VLSI15 Material Handling & Lot Flow**  
**Description:** Routes/schedules AMHS/AGVs for wafer lots avoiding delays in re-entrant flow. [sciencedirect](https://www.sciencedirect.com/science/article/abs/pii/S0360835216300821)
**Template:** Vehicle routing + synchronization | MIP, simulation.  
**Relevance:** Priority: High | Fab logistics backbone.  
**Hardness:** Class: NP-hard | VRPTW generalization.  
**Dependencies:** Upstream: VLSI12–VLSI13 | Downstream: VLSI12–VLSI13.  
**Comments:** OHT/AGV conflicts | #ops #route ##AMHS ##fab-flow

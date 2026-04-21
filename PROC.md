**PROC (Continuous/Process Manufacturing Systems)**  
========================================================  

**Scope:**  
Continuous and batch process industries (chemicals, pharma, food, refining, polymers). Exclude discrete manufacturing (handled in PROD). Focus on combinatorial decisions (e.g., sequencing campaigns, recipe-unit assignment), not continuous control, simulation, or purely convex programs. [pubs.acs](https://pubs.acs.org/doi/abs/10.1021/ie403129y)

--------------------------------------------------------  
**1) DESIGN / STRUCTURAL CONFIGURATION**  
--------------------------------------------------------  

**PROC01 Process Network Design**  
**Description:** Selects and interconnects processing units, pipelines, and storage to meet production capacity and product slate under capital constraints. [pubs.acs](https://pubs.acs.org/doi/abs/10.1021/ie801001q)
**Template:** Multisite facility location + network flow design | MIP, MINLP decomposition.  
**Relevance:** Priority: Critical | Capital-intensive decisions defining plant topology in refineries and chemicals. [pubs.acs](https://pubs.acs.org/doi/abs/10.1021/ie801001q)  
**Hardness:** Class: NP-hard | Facility location and network design are NP-hard. [pubs.acs](https://pubs.acs.org/doi/abs/10.1021/ie801001q)  
**Dependencies:** Upstream: — | Downstream: PROC05, PROC11.  
**Comments:** Long-term structural choices | #des #config ##network-design ##refinery  

**PROC02 Recipe-Structure Configuration**  
**Description:** Defines production recipes selecting unit procedures, equipment classes, and material balances for product variants. [blogs.sw.siemens](https://blogs.sw.siemens.com/consumer-products-retail/2025/03/28/adapt-and-scale-faster-when-you-centralize-and-streamline-recipe-management/)
**Template:** Recipe assignment + compatibility selection | CP-SAT, MIP.  
**Relevance:** Priority: High | Core in batch pharma/food for scalability and compliance.  
**Hardness:** Class: NP-hard | Assignment with alternatives generalizes set-cover.  
**Dependencies:** Upstream: — | Downstream: PROC08, PROC11, PROC15.  
**Comments:** ISA-88 compliant master recipes | #des #config ##recipes ##ISA88  

--------------------------------------------------------  
**2) PLANNING (Demand, Material, Release Intent)**  
--------------------------------------------------------  

**PROC03 Multi-Product Production Planning**  
**Description:** Allocates production quantities across products and time periods under capacity, inventory, and demand constraints. [gor-ev](http://www.gor-ev.de/wp-content/uploads/2016/08/tg81.pdf)
**Template:** Multi-period multi-commodity planning | MIP, rolling-horizon.  
**Relevance:** Priority: Critical | Aggregates demand to campaign intent in continuous plants. [gor-ev](http://www.gor-ev.de/wp-content/uploads/2016/08/tg81.pdf)  
**Hardness:** Class: NP-hard | Capacitated multi-item planning NP-hard.  
**Dependencies:** Upstream: PROC01, PROC02 | Downstream: PROC11, PROC14.  
**Comments:** Links sales to plant feasibility | #plan #select ##production-planning  

**PROC04 Campaign Planning**  
**Description:** Determines production campaigns (sequences of product lots) to meet demand while minimizing changeovers over planning horizon. [anderson.ucla](https://www.anderson.ucla.edu/documents/areas/fac/dotm/bio/pdf_KR15.pdf)
**Template:** Multi-period sequencing + lot-sizing | MIP, decomposition.  
**Relevance:** Priority: Critical | Standard in food/pharma/bioprocess for multi-product plants. [anderson.ucla](https://www.anderson.ucla.edu/documents/areas/fac/dotm/bio/pdf_KR15.pdf)  
**Hardness:** Class: NP-hard | Campaign sequencing embeds TSP-like problems.  
**Dependencies:** Upstream: PROC03 | Downstream: PROC15, PROC16.  
**Comments:** Balances inventory and setups | #plan #select ##campaigns ##multi-product  

**PROC05 Raw Material Procurement & Blending Planning**  
**Description:** Selects supplier lots and blends to meet recipe specs and inventory targets under quality constraints. [aspentech](https://www.aspentech.com/en/resources/blog/why-chemicals-producers-cant-afford-to-overlook-production-scheduling)
**Template:** Multi-blend knapsack + assignment | MIP.  
**Relevance:** Priority: High | Critical in refining/polymers for feedstock optimization.  
**Hardness:** Class: NP-hard | Blend selection generalizes knapsack.  
**Dependencies:** Upstream: PROC01 | Downstream: PROC11.  
**Comments:** Quality-constrained procurement | #plan #alloc ##blending ##feedstock  

--------------------------------------------------------  
**3) RESOURCE ALLOCATION (Calendars, Matching, Assignment)**  
--------------------------------------------------------  

**PROC06 Operator Task Assignment**  
**Description:** Assigns operators to process units/shifts under skill, coverage, and regulatory constraints. [bigfuture.collegeboard](https://bigfuture.collegeboard.org/careers/chemical-plant-and-system-operator/tasks-knowledge-skills)
**Template:** Skill-constrained rostering/assignment | CP-SAT, column-gen.  
**Relevance:** Priority: High | Safety-critical in staffed chemical/pharma plants.  
**Hardness:** Class: NP-hard | Nurse rostering generalization.  
**Dependencies:** Upstream: PROC03 | Downstream: PROC15, PROC16.  
**Comments:** Human factors in continuous ops | #alloc #skills ##operators ##rostering  

**PROC07 Utility & Energy Allocation**  
**Description:** Allocates shared utilities (steam, power) across units under peak-demand and calendar constraints. [sciencedirect](https://www.sciencedirect.com/science/article/pii/S0167637723001049)
**Template:** Resource-constrained allocation | MIP.  
**Relevance:** Priority: Medium | Binding in energy-intensive refining/chemicals.  
**Hardness:** Class: NP-hard | Resource matching NP-hard. [sciencedirect](https://www.sciencedirect.com/science/article/pii/S0167637723001049)  
**Dependencies:** Upstream: — | Downstream: PROC15.  
**Comments:** Shared resource overlay | #alloc ##utilities ##energy  

**PROC08 Unit Cleaning & Availability Calendars**  
**Description:** Schedules cleaning/turnaround windows for units to manage contamination risks. [aspentech](https://www.aspentech.com/en/resources/blog/why-chemicals-producers-cant-afford-to-overlook-production-scheduling)
**Template:** Calendar-constrained scheduling | MIP, CP-SAT.  
**Relevance:** Priority: High | Essential for product purity in pharma/food.  
**Hardness:** Class: NP-hard | Preemptive scheduling with windows.  
**Dependencies:** Upstream: PROC02 | Downstream: PROC15, PROC16.  
**Comments:** Hygiene constraint layer | #alloc #calendars ##cleaning ##CIP  

**PROC09 Maintenance Campaign Planning**  
**Description:** Plans shutdown scopes and timings across units to balance reliability and production loss. [youtube](https://www.youtube.com/watch?v=6i8XliHzL2w)
**Template:** Multi-resource project scheduling | MIP.  
**Relevance:** Priority: High | Major downtime driver in continuous plants. [youtube](https://www.youtube.com/watch?v=6i8XliHzL2w)  
**Hardness:** Class: NP-hard | RCPSP generalization. [youtube](https://www.youtube.com/watch?v=6i8XliHzL2w)  
**Dependencies:** Upstream: PROC03 | Downstream: PROC15.  
**Comments:** Opportunistic turnarounds | #alloc #calendars ##maintenance ##shutdown  

--------------------------------------------------------  
**4) OPERATIONS (Scheduling, Sequencing, Flow)**  
--------------------------------------------------------  

**PROC10 Recipe-Unit Assignment**  
**Description:** Assigns recipes (products) to processing units considering compatibility and capacity. [pubs.acs](https://pubs.acs.org/doi/abs/10.1021/ie403129y)
**Template:** Generalized assignment | MIP, CP-SAT.  
**Relevance:** Priority: High | Multi-product/multi-train allocation.  
**Hardness:** Class: NP-hard | Assignment with side-constraints.  
**Dependencies:** Upstream: PROC02, PROC04, PROC08 | Downstream: PROC15.  
**Comments:** Product-train matching | #ops #alloc ##assignment ##multi-mode  

**PROC11 Lot/Batch Sizing & Release**  
**Description:** Determines discrete lot sizes/timings under setups, storage, and capacity limits. [pubs.acs](https://pubs.acs.org/doi/abs/10.1021/ie403129y)
**Template:** Capacitated lot-sizing (CLSP variants) | MIP, DP.  
**Relevance:** Priority: Critical | Drives inventory and changeover costs.  
**Hardness:** Class: NP-hard | CLSP NP-hard.  
**Dependencies:** Upstream: PROC03, PROC04, PROC05, PROC10 | Downstream: PROC15, PROC16.  
**Comments:** Discrete release to execution | #ops #flow ##lot-sizing  

**PROC12 Sequence-Dependent Campaign Scheduling**  
**Description:** Sequences production campaigns on single train/unit with changeover times/ costs. [aspentech](https://www.aspentech.com/en/resources/blog/why-chemicals-producers-cant-afford-to-overlook-production-scheduling)
**Template:** TSP/sequencing with setups | CP-SAT, LNS.  
**Relevance:** Priority: Critical | Dominant cost in polymers/food grade changes. [aspentech](https://www.aspentech.com/en/resources/blog/why-chemicals-producers-cant-afford-to-overlook-production-scheduling)  
**Hardness:** Class: NP-hard | TSP-hard.  
**Dependencies:** Upstream: PROC04, PROC11, PROC08, PROC09 | Downstream: PROC17.  
**Comments:** Changeover minimization kernel | #ops #sched ##changeovers ##campaign-seq  

**PROC13 Parallel Train Scheduling**  
**Description:** Schedules and sequences campaigns across parallel identical/unrelated processing trains. [sciencedirect](https://www.sciencedirect.com/science/article/pii/S0167637723001049)
**Template:** Parallel machine batch scheduling | CP-SAT, MIP. [sciencedirect](https://www.sciencedirect.com/science/article/pii/S0167637723001049)  
**Relevance:** Priority: Critical | Standard in refining multi-train ops. [sciencedirect](https://www.sciencedirect.com/science/article/pii/S0167637723001049)  
**Hardness:** Class: NP-hard | P||Cmax NP-hard. [sciencedirect](https://www.sciencedirect.com/science/article/pii/S0167637723001049)  
**Dependencies:** Upstream: PROC04, PROC11, PROC06, PROC07, PROC08, PROC09 | Downstream: PROC17.  
**Comments:** Load-balancing across capacity | #ops #sched ##parallel-trains  

**PROC14 Batch Process Scheduling**  
**Description:** Schedules discrete batches through multi-stage recipe networks with resources/stages. [pubs.acs](https://pubs.acs.org/doi/abs/10.1021/ie403129y)
**Template:** Multipurpose batch plant scheduling | STN/MTZN MIP.  
**Relevance:** Priority: Critical | Pharma/food batch core model. [pubs.acs](https://pubs.acs.org/doi/abs/10.1021/ie403129y)  
**Hardness:** Class: NP-hard | JSS generalization.  
**Dependencies:** Upstream: PROC02, PROC11, PROC06, PROC08 | Downstream: PROC17.  
**Comments:** Batch-specific routing | #ops #sched ##batch-plant ##STN  

**PROC15 Continuous Campaign Synchronization**  
**Description:** Synchronizes start/end times, rates, and transfers across continuous units to avoid shortages/blocking. [gor-ev](http://www.gor-ev.de/wp-content/uploads/2016/08/tg81.pdf)
**Template:** Resource-constrained flow scheduling | CP-SAT, MIP.  
**Relevance:** Priority: High | Ensures feasible continuous flows.  
**Hardness:** Class: NP-hard | Synchronization embeds RCPSP.  
**Dependencies:** Upstream: PROC10–PROC14 | Downstream: PROC12–PROC14.  
**Comments:** Physics-meets-scheduling | #ops #flow ##synchronization ##continuous  

**PROC16 Storage Tank Allocation & Blending**  
**Description:** Assigns products to tanks and blends during transfers under segregation/contamination rules. [aspentech](https://www.aspentech.com/en/resources/blog/why-chemicals-producers-cant-afford-to-overlook-production-scheduling)
**Template:** Tank assignment + sequencing | MIP, CP-SAT.  
**Relevance:** Priority: High | Bottleneck in refining/chemicals inventory.  
**Hardness:** Class: NP-hard | Assignment + TSP.  
**Dependencies:** Upstream: PROC11, PROC12 | Downstream: PROC15.  
**Comments:** Intermediate storage constraints | #ops #alloc ##tanks ##blending
This diagram illustrates classic combinatorial problems like sequencing and assignment, which underpin PROC challenges such as campaign sequencing and resource matching in process plants. [myplan](https://www.myplan.com/careers/chemical-plant-and-system-operators/description-51-8091.00.html)

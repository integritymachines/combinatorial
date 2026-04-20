========================================================
PROD  (Discrete Manufacturing Systems)
========================================================

Scope:
Discrete manufacturing systems including job shops, flow lines, assembly lines,
flexible manufacturing systems (FMS), and mixed-model production.
Continuous/process manufacturing is explicitly excluded (handled under PROC).

The domain covers architectural decisions, planning, execution, and evolution of
physical production systems with discrete jobs, machines, and resources.


1. SYSTEM & PROCESS DESIGN

Definition of the production system structure and logic.
Decisions here constrain all downstream planning and execution problems.

Includes:
- process type selection (job shop, flow shop, line, cell, FMS)
- routing and operation structure
- system layout and material flow topology
- precedence and process constraints
- manufacturability and flexibility trade-offs


2. CAPACITY & INVESTMENT

Long- to mid-term commitment of production resources.

Includes:
- machine and equipment selection
- capacity sizing and redundancy
- tooling and automation level decisions
- bottleneck identification and mitigation
- expansion, contraction, and substitution options


3. PRODUCTION PLANNING

Mid-term planning that translates demand into feasible production targets.

Includes:
- multi-level production planning
- master production scheduling (MPS)
- lot sizing and batching
- demand allocation and feasibility
- order acceptance and prioritization


4. SCHEDULING, SEQUENCING & EXECUTION

Detailed operational control of jobs, machines, and resources.

Includes:
- single and parallel machine sequencing
- job shop, flow shop, hybrid shop scheduling
- assembly line balancing and sequencing
- setup, changeover, and batch sequencing
- integrated scheduling with transport and maintenance
- real-time dispatching and exception handling

(This section will host the majority of canonical NP-hard scheduling problems.)


5. QUALITY & MAINTENANCE

Decisions that ensure yield, availability, and reliability.

Includes:
- inspection placement and sampling
- rework and scrap routing
- preventive and corrective maintenance planning
- maintenance-integrated scheduling
- spare parts and maintenance resource allocation


6. WORKFORCE & OPERATIONS SUPPORT

Human resources and supporting operational decisions tightly coupled to production.

Includes:
- operator assignment and skill matching
- shift and crew scheduling
- labor-machine coupling
- learning, absenteeism, and robustness policies


7. FLOW CONTROL & INTERNAL LOGISTICS

Control of material flow within the production system.

Includes:
- buffer sizing and placement
- WIP control policies (pull / push)
- palletization and part-family grouping
- internal transport and AGV routing
- synchronization of machines, buffers, and transport


8. RECONFIGURATION, IMPROVEMENT & ROBUSTNESS

Adaptation of the production system over time.

Includes:
- line rebalancing and layout reconfiguration
- capacity migration and technology upgrades
- ramp-up / ramp-down planning
- disruption recovery and resilience design
- continuous improvement and redesign policies


Notes:
- Individual PROD## problems will be introduced within these sections.
- Numbering will follow contingency precedence, not chronology.
- Closed (#tag) and open (##tag) tagging is applied only at problem level.

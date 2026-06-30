Industrial Combinatorial Optimization Ontology
v0.3: 24 June 2026

Legend

CLUSTER -> DOMAIN
DOMAIN -> SUBDOMAIN
DOMAIN <-> DOMAIN    recurring interface or ambiguous boundary
DOMAIN ? DOMAIN      unresolved or context-dependent ownership

CLUSTERS -> DOMAINS
#TRANS -> #PROC, #PROD
#DISPL -> #LOG, #SCM
#INFRA -> #ENER, #CIVIC
#EXCH  -> #MKT, #FIN
#HUMAN -> #HC, #HR
#INFO  -> #COMP, #INTEL
#RES   -> #EXTR, #LAND


1. TRANSFORMATION (#TRANS)
Transformation = systems that change material or product state.
#TRANS -> #PROC, #PROD

#PROC Continuous & Batch Process Manufacturing Systems
#PROC -> Refining
#PROC -> Petrochemicals
#PROC -> Specialty chemicals
#PROC -> Industrial gases
#PROC -> Polymers
#PROC -> Food & beverage process systems
#PROC -> Pharmaceutical batch manufacturing
#PROC -> Bioprocessing / fermentation
#PROC -> Pulp & paper
#PROC -> Cement
#PROC -> Glass
#PROC -> Steelmaking, process side
#PROC -> Semiconductor wet process / deposition process layers

#PROC -> STN/RTN scheduling
#PROC -> Campaign scheduling
#PROC -> Blending and pooling
#PROC -> Tank farm allocation
#PROC -> Grade transitions
#PROC -> Utility-aware scheduling
#PROC -> CIP scheduling
#PROC -> Batch genealogy and contamination control
#PROC -> Recipe-unit assignment
#PROC -> Zero-wait scheduling
#PROC -> Pipeline transfer synchronization

#PROC <-> #PROD     semiconductor fabs, pharma packaging
#PROC <-> #ENER     industrial utilities
#PROC <-> #LOG      bulk logistics terminals
#PROC <-> #SCM      process supply networks

Specialized-domain candidates:
#PROC -> Refinery operations
#PROC -> Pharmaceutical process manufacturing
#PROC -> Semiconductor process operations

#PROD Discrete Production & Assembly Systems
#PROD -> Automotive manufacturing
#PROD -> Aerospace manufacturing
#PROD -> Electronics assembly
#PROD -> Semiconductor fabs
#PROD -> Industrial equipment manufacturing
#PROD -> Appliance manufacturing
#PROD -> Contract manufacturing
#PROD -> Additive manufacturing systems
#PROD -> Shipbuilding
#PROD -> Defense manufacturing
#PROD -> Battery pack assembly

#PROD -> Flexible job shops
#PROD -> Hybrid flow shops
#PROD -> Reentrant scheduling
#PROD -> Tool-constrained scheduling
#PROD -> Secondary-resource scheduling
#PROD -> Assembly balancing
#PROD -> WIP control
#PROD -> Release planning
#PROD -> Maintenance-production integration
#PROD -> Semiconductor batching
#PROD -> Changeover optimization

#PROD <-> #PROC     semiconductor fabs, battery chemistry operations
#PROD <-> #INFRA    construction projects
#PROD <-> #HR       field-service assembly
#PROD <-> #LOG      warehouse kitting
#PROD <-> #COMP     semiconductor systems, VLSI implementation

Specialized-domain candidates:
#PROD -> Semiconductor manufacturing
#PROD -> Aerospace production systems
#PROD -> Electronics manufacturing systems


2. DISPLACEMENT (#DISP)
Displacement = systems that move goods, people, inventory, or service capacity through space or time.
#DISP -> #LOG, #SCM

#LOG Logistics & Transportation Systems
#LOG -> Parcel delivery
#LOG -> LTL/TL freight
#LOG -> Maritime shipping
#LOG -> Tanker logistics
#LOG -> Rail freight
#LOG -> Airline operations
#LOG -> Ride-hailing
#LOG -> Grocery delivery
#LOG -> Field service routing
#LOG -> Warehouse fulfillment
#LOG -> Cold-chain logistics
#LOG -> Port operations
#LOG -> Airport airside operations
#LOG -> Drone logistics

#LOG -> VRPTW
#LOG -> Pickup-and-delivery
#LOG -> Dynamic dispatch
#LOG -> Airline recovery
#LOG -> Gate/stand assignment
#LOG -> Crew routing
#LOG -> Crossdock scheduling
#LOG -> Order batching and picker routing
#LOG -> Empty repositioning
#LOG -> Fleet assignment
#LOG -> Multi-modal routing

#LOG <-> #HR        airline crew legality, driver duty design
#LOG <-> #INFRA     public transit, shared right-of-way
#LOG <-> #SCM       inventory-routing, replenishment transport
#LOG <-> #HC        ambulance relocation
#LOG <-> #INTEL       defense logistics and security overlays

Specialized-domain candidates:
#LOG -> Airline operations
#LOG -> Warehouse operations
#LOG -> Last-mile delivery systems

#SCM Supply Chain & Inventory Systems
#SCM -> Consumer supply chains
#SCM -> Industrial distribution
#SCM -> Omni-channel retail networks
#SCM -> Spare-parts systems
#SCM -> Chemical supply networks
#SCM -> Pharma supply chains
#SCM -> Retail replenishment systems
#SCM -> Supplier network design
#SCM -> S&OP / IBP systems
#SCM -> Global sourcing systems

#SCM -> Multi-echelon inventory
#SCM -> Facility location
#SCM -> Inventory positioning
#SCM -> ATP/CTP
#SCM -> Deployment planning
#SCM -> Replenishment optimization
#SCM -> Allocation under shortage
#SCM -> Supply network resilience
#SCM -> Service-level optimization
#SCM -> Inventory-routing integration

#SCM <-> #LOG       warehouse execution, shipment execution
#SCM <-> #PROC      production feasibility
#SCM <-> #PROD      production feasibility
#SCM <-> #MKT       assortment, promotion, ATP
#SCM <-> #FIN       working capital
#SCM <-> #HR        spare-parts field service
#SCM <-> #LAND      agricultural and real-estate supply networks
#SCM <-> #EXTR      extracted-resource supply networks

Specialized-domain candidates:
#SCM -> Retail supply networks
#SCM -> Spare-parts optimization
#SCM -> Omni-channel fulfillment systems


3. INFRASTRUCTURE (#INFRA)
Infrastructure = shared physical service substrates and utility systems.
#INFRA -> #ENER, #CIVIC

#ENER Energy & Utility Systems
#ENER -> Power systems
#ENER -> ISO/RTO operations
#ENER -> Water utilities
#ENER -> Gas transmission
#ENER -> District heating/cooling
#ENER -> Renewable integration
#ENER -> Microgrids
#ENER -> VPP aggregation
#ENER -> Industrial utility systems
#ENER -> Battery storage coordination

#ENER -> SCUC/SCED
#ENER -> Outage scheduling
#ENER -> Reserve co-optimization
#ENER -> Pump scheduling
#ENER -> Hydro scheduling
#ENER -> Storage dispatch
#ENER -> Transmission switching
#ENER -> Congestion management
#ENER -> Grid restoration
#ENER -> DER aggregation

#ENER <-> #CIVIC    water infrastructure maintenance
#ENER <-> #PROC     industrial utilities
#ENER <-> #PROD     energy-aware production
#ENER <-> #FIN      renewable asset portfolios, hedging
#ENER <-> #EXTR     fuel extraction
#ENER <-> #LAND     water management, land-use constraints
#ENER <-> #COMP     telecom-energy and data-center energy coordination

Specialized-domain candidates:
#ENER -> Power system operations
#ENER -> Water utility optimization
#ENER -> Distributed energy coordination

#CIVIC Civic Infrastructure & Construction
#CIVIC -> Public transit
#CIVIC -> Municipal waste
#CIVIC -> Road maintenance
#CIVIC -> Public works
#CIVIC -> Parking systems
#CIVIC -> Water-service maintenance
#CIVIC -> Airport landside systems
#CIVIC -> Smart-city coordination
#CIVIC -> Public facility maintenance
#CIVIC -> Construction project interfaces

#CIVIC -> Timetabling
#CIVIC -> Vehicle scheduling
#CIVIC -> Crew scheduling
#CIVIC -> Arc routing
#CIVIC -> Work-zone planning
#CIVIC -> Maintenance-window coordination
#CIVIC -> Public-service coverage
#CIVIC -> Transit synchronization
#CIVIC -> Waste collection routing
#CIVIC -> Construction staging

#CIVIC <-> #LOG      airline airside operations, public transit interfaces
#CIVIC <-> #ENER     utility dispatch and water-service infrastructure
#CIVIC <-> #INTEL    public safety response
#CIVIC <-> #HR       generic field crews
#CIVIC <-> #LAND     urban land-use, real estate, geospatial assets
#CIVIC <-> #PROD     construction production, prefabrication

Specialized-domain candidates:
#CIVIC -> Transit operations
#CIVIC -> Municipal service systems
#CIVIC -> Infrastructure maintenance systems
#CIVIC -> Construction planning systems



4. EXCHANGE (#EXCH)
Exchange = systems that allocate, transfer and exchange goods, services, information, rights or claims.
#EXCH -> #MKT, #FIN

#MKT Market & Commercial Allocation Systems
#MKT -> Revenue management
#MKT -> Retail assortment
#MKT -> Ad-tech allocation
#MKT -> Procurement auctions
#MKT -> Marketplace ranking systems
#MKT -> Dynamic offer systems
#MKT -> Promotions optimization
#MKT -> Yield management
#MKT -> Media scheduling
#MKT -> Capacity allocation markets

#MKT -> Assortment optimization
#MKT -> Ad allocation
#MKT -> Winner determination
#MKT -> Dynamic availability control
#MKT -> Auction clearing
#MKT -> Slot allocation
#MKT -> Promotion optimization
#MKT -> Matching markets
#MKT -> Bid pacing
#MKT -> Contract allocation

#MKT <-> #LOG       airline seat inventory, service windows
#MKT <-> #SCM       inventory-constrained retail, availability
#MKT <-> #FIN       financial exchanges
#MKT <-> #HR        labor marketplaces
#MKT <-> #COMP      cloud pricing, ad-tech infrastructure

Specialized-domain candidates:
#MKT -> Ad-tech systems
#MKT -> Airline/hospitality revenue management
#MKT -> Combinatorial auction systems

#FIN Financial and Reporting Systems
#FIN -> Treasury systems
#FIN -> Collateral optimization
#FIN -> Settlement systems
#FIN -> Clearing systems
#FIN -> Corporate cash management
#FIN -> Portfolio optimization with discreteness
#FIN -> CCP operations
#FIN -> Liquidity management
#FIN -> Funding allocation
#FIN -> Securities lending

#FIN -> Collateral allocation
#FIN -> Settlement queue optimization
#FIN -> Cash pooling
#FIN -> Funding optimization
#FIN -> Netting optimization
#FIN -> Liquidity allocation
#FIN -> Portfolio cardinality optimization
#FIN -> Treasury transfer optimization

#FIN <-> #SCM       commodity trading logistics, working capital
#FIN <-> #LOG       commodity movement and delivery settlement
#FIN <-> #RES       real-estate finance
#FIN <-> #MKT       market auctions and exchanges
#FIN <-> #ENER      power trading
#FIN <-> #COMP      crypto and digital settlement infrastructure

Specialized-domain candidates:
#FIN -> Post-trade optimization
#FIN -> Treasury optimization systems
#FIN -> Clearinghouse operations

5. HUMAN (#HUMAN)
Human = systems where human capability or human-critical service feasibility dominates.
#HUMAN -> #HC, #HR

#HC Healthcare & Human-Critical Operational Systems
#HC -> Perioperative systems
#HC -> Inpatient flow
#HC -> Emergency medical services
#HC -> Home healthcare
#HC -> Ambulatory scheduling
#HC -> Blood logistics
#HC -> ICU capacity management
#HC -> Oncology scheduling
#HC -> Dialysis systems
#HC -> Disaster medical response

#HC -> OR scheduling
#HC -> Bed management
#HC -> Ambulance relocation
#HC -> Appointment scheduling
#HC -> Care pathway coordination
#HC -> Home-health routing
#HC -> Staff-patient synchronization
#HC -> Admission control

#HC <-> #HR         generic rostering, clinical staffing
#HC <-> #SCM        medical supply chains
#HC <-> #LOG        ambulance routing, patient transport
#HC <-> #CIVIC      public health infrastructure
#HC <-> #INTEL      military medicine and disaster response

Specialized-domain candidates:
#HC -> Hospital operations
#HC -> EMS systems
#HC -> Home-health coordination

#HR Workforce & Human Resource Organization
#HR -> Field service
#HR -> Retail/service staffing
#HR -> Aviation crew systems
#HR -> Utilities field crews
#HR -> Technician routing
#HR -> Call-center workforce management
#HR -> Contractor coordination
#HR -> Gig-workforce systems

#HR -> Rostering
#HR -> Crew pairing
#HR -> Technician routing
#HR -> Shift generation
#HR -> Fairness optimization
#HR -> Skill matching
#HR -> Overtime control
#HR -> Break scheduling

#HR <-> #HC         clinical staffing
#HR <-> #LOG        driver routing, crew legality
#HR <-> #MKT        labor marketplaces
#HR <-> #COMP       workforce platforms, digital work queues
#HR <-> #INFRA      public-service staffing

Specialized-domain candidates:
#HR -> Airline crew systems
#HR -> Field-service systems
#HR -> Workforce marketplaces


6. INFORMATION (#INFO)
Information = systems where sensing, computation, coordination, or adversarial information dominates.
#INFO -> #COMP, #INTEL

#COMP Computational & Digital Systems
#COMP -> Cloud orchestration
#COMP -> Container scheduling
#COMP -> Edge computing
#COMP -> CDNs
#COMP -> NFV/telecom core
#COMP -> HPC scheduling
#COMP -> Datacenter operations
#COMP -> GPU/accelerator allocation
#COMP -> Distributed storage systems
#COMP -> AI infrastructure systems

#COMP -> Cluster scheduling
#COMP -> Placement
#COMP -> Autoscaling
#COMP -> Traffic engineering
#COMP -> Service chaining
#COMP -> Replica placement
#COMP -> Queue admission
#COMP -> Accelerator allocation
#COMP -> VM migration
#COMP -> Multi-tenant fairness

#COMP <-> #CIVIC    telecom infrastructure
#COMP <-> #MKT      ad allocation and marketplaces
#COMP <-> #INTEL    cyber and adversarial systems
#COMP <-> #ENER     power-aware compute
#COMP <-> #FIN      AI training economics, crypto infrastructure

Specialized-domain candidates:
#COMP -> Cloud infrastructure systems
#COMP -> Telecom core optimization
#COMP -> AI infrastructure orchestration

#INTEL Intelligence, Defense & Security Systems
#INTEL -> Homeland security
#INTEL -> Border inspection
#INTEL -> Satellite tasking
#INTEL -> ISR coordination
#INTEL -> Patrol systems
#INTEL -> Strategic inspection systems
#INTEL -> Critical infrastructure protection
#INTEL -> Military surveillance systems
#INTEL -> Maritime security
#INTEL -> Air defense coordination

#INTEL -> Patrol scheduling
#INTEL -> Security games
#INTEL -> Satellite observation scheduling
#INTEL -> Interdiction planning
#INTEL -> Inspection allocation
#INTEL -> Randomized coverage
#INTEL -> Surveillance routing
#INTEL -> Resource denial planning

#INTEL <-> #LOG       generic logistics
#INTEL <-> #HC        disaster response
#INTEL <-> #CIVIC     public safety and critical infrastructure protection
#INTEL <-> #COMP      cyber infrastructure
#INTEL <-> #HR        intelligence staffing
#INTEL <-> #EXTR     resource surveillance
#INTEL <-> #LAND     land-use intelligence and geospatial monitoring

Specialized-domain candidates:
#INTEL -> Satellite operations
#INTEL -> Security-game systems
#INTEL -> ISR coordination systems


7. RESOURCE (#RES)
Resource = systems that extract, harvest, activate, or allocate natural and geospatial assets.
#RES -> #EXTR, #LAND

#EXTR Resource Extraction 
#EXTR -> Open-pit mining
#EXTR -> Underground mining interfaces
#EXTR -> Mine scheduling
#EXTR -> Prospecting
#EXTR -> Water prospecting
#EXTR -> Water extraction
#EXTR -> Oil and gas field development
#EXTR -> Quarrying
#EXTR -> Ore blending and destination planning

#EXTR -> Block scheduling
#EXTR -> Extraction sequencing
#EXTR -> Prospect selection
#EXTR -> Drilling campaign planning
#EXTR -> Haulage dispatch
#EXTR -> Grade control
#EXTR -> Destination assignment
#EXTR -> Resource depletion planning

#EXTR <-> #LAND     land access, water management, reclamation, environmental constraints
#EXTR <-> #SCM      extracted-resource supply chains
#EXTR <-> #ENER     fuel supply, energy demand, water-energy coupling
#EXTR <-> #LOG      haulage and transport
#EXTR <-> #INTEL    remote sensing, surveillance, prospecting intelligence
#EXTR <-> #FIN      commodity finance and project finance

Specialized-domain candidates:
#EXTR -> Mining
#EXTR -> Prospecting
#EXTR -> Oil and gas field development

#LAND Land-Use and Agriculture
#LAND -> Forestry
#LAND -> Agriculture
#LAND -> Fisheries
#LAND -> Water management
#LAND -> Water-right allocation
#LAND -> Land-use systems
#LAND -> Real estate systems
#LAND -> Biomass harvesting
#LAND -> Reclamation sequencing
#LAND -> Urban land-use systems

#LAND -> Harvest scheduling
#LAND -> Spatial adjacency optimization
#LAND -> Field-operation routing
#LAND -> Crop rotation planning
#LAND -> Land-use allocation
#LAND -> Development phasing
#LAND -> Tenant allocation
#LAND -> Water allocation
#LAND -> Watershed and basin planning
#LAND -> Reclamation sequencing

#LAND <-> #CIVIC    construction sequencing, urban land-use, civic planning
#LAND <-> #PROD     construction production, prefabrication
#LAND <-> #SCM      biofuel supply chains, agricultural supply chains
#LAND <-> #ENER     utility-scale renewables, hydrology-energy interactions
#LAND <-> #COMP     smart agriculture operations, geospatial analytics
#LAND <-> #FIN      real-estate finance, land-backed claims
#LAND <-> #MKT      tenant mix and commercial allocation

Specialized-domain candidates:
#LAND -> Forestry systems
#LAND -> Real estate systems
#LAND -> Agricultural operations
#LAND -> Water management systems


CROSS-CUTTING STRUCTURAL CLUSTERS
These structures recur across many domains and should not themselves define domains.

Strongly cross-domain:
- Scheduling
- Matching
- Covering
- Resource allocation
- Set partitioning
- Dynamic dispatch
- Rolling horizon repair
- Robust optimization
- Stochastic planning
- Simulation-optimization

Cross-domain industrial motifs:
- Secondary-resource coupling
- Sequence-dependent setups
- Legal-pattern generation
- Spatial adjacency
- Synchronization constraints
- State propagation
- Multiobjective tradeoffs
- Human override / repair
- Real-time recourse


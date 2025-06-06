
# STP
- prevent layer 2 loops, broadcast storms
- does this by building loop free network by logically blocking redundant links
- how does STP work
	1. elect root bridge, lowest BID (composed of priority, mac address). Lower number wins. Default priority is 32768. First priority, if tie, then mac address. Usually, older devices have lower mac addresses, so we should choose our priority. Priority increments by 4096, max priority is 61440.
	2. To determine root bridge, switches communicate using BPDU (Bridge protocol data unit). 
- Root port - lowest cost to the root bridge, 1 root port per switch. Faces towards the root bridge
- Designated port - active port, but not root bridge
- Blocked port - disabled port to prevent loop
- STP Port Speed Costs
	- 10 Mbps - 100
	- 100 Mbps - 19
	- 1 gbps - 4
	- 10 gbps - 2
	- 10+ gbps - 1
- Port States
	- Blocked (20s) - blocked port, but can receive BPDUs. When device first connected, it will be in blocking state
	- Listening (15s) - blocked, but is sending BPDUs
	- learning (15s) - blocked, but populating max table
	- forward  - normal forwarding state
- RSTP - new port roles and states, combines blocked and listening states to save 20 s
- PVST+ (Per VLAN Spanning Tree) - cisco proprietary, can be used to load balance
- STP port extensions
	- Spanning tree portfast - goes straight into forwarding
		- conf t, int interface, spanning-tree portfast
		- spanning-tree portfast default
	- BPDU guard: used in conjunction with portfast. If this port receives a BPDU, it goes into err disabled. Need to shut/no shut to reactivate.
		- spanning-tree bpduguard


## EIGRP
- pros: full redundancy, scalable, easy to manage
- cons: less control, more complex
- distance vector: distance (length) + vector(direction). Also known as routing by rumor
- link state: complete knowledge of the network
- This is cisco proprietary
- Admin distance of 90
- Utilizes AS number, completely arbitrary
- Maintains 3 tables: each router calculates best path based on info provided by neighbor
	- neighbor:
	- topology: 
	- routing: 
- Network statements:
	- which int to accept traffic in
	- which int to send traffic out 
	- what int subnet to advertise
	- utilizes wildcard mask: opposite of subnet mask
	- help form neighbor relationships, must match AS system number and subnet mask
- If parameters match, begin sharing topology tables and routes, if do not match, then no neighbor relationship is formed
- Passive interfaces: interfaces that you do not want to form neigborships on, it will not send hello messages to discover neighbors. The interface subnet is still advertised tho
	- router eigrp 50, passive-int g0/1
	- router eigrp 50, passive-int default, no passive-int g0/3
- to do default route, must already have default route in routing table. Then you can redistribute. 


## OSPF
- link stae protocol, admin distance of 110
- each router has complete map of network topology, each router will calculate the best path for each packet
- Process ID is locally significant identifier
- OSPF Areas: segment network in hierarchy 
	- Limit impact of network changes: only routers in an area will have to make the change
	- area 0 is backbone, it must exist, all other areas must attach to area 0
- Backbone router: any router in area 0
- area border router: sits between area 0 and other areas
- internal router: router in an area other than area 0
- AS boundary router: has 2 routing protocols, between different dynamic routing protocols
- Network states: which ints accept traffic in, which ints to send out traffic, and which subnets to advertise.
- OSPF neighbors: connected L3 devices share their routes
	- relationship formed through matching network statements
	- parameters must match: process ID, area ID, subnet mask
- Database: composed of LSA (link state advertisements)
	- shared via LSU (link state updates)
	- for each area: unique database, each router has a copy, ABRs have database for each area
- Passive interfaces: ints that do not form neighbors
	- interface will not send hellos
	- interface subnet will still be added to OSPF database
	- router ospf 50, passive-int g0/1
	- to do default passive ints
		- router ospf 50, passive-int default, no passive-int g0/3
- Default route: must have default route in routing table, via static, bgp, whatever
	- default route injected as type 5 LSA
	- only need to do this on one router in the area
	- router ospf 50, default-info originate
- ospf has redistribution metric by default
	- use "subnets" keyword
	- router ospf 100, redistribute static subnets
	- router ospf 100, redistribute eigrp 75 subnets
- LSA
	- type 1 router LSA: represents a router and connected interfaces, intra area
	- type 3 summary LSA: a network between two routers, inter area
	- type 5 external LSA: a route imported into OSPF from another protocol
	- type 7 NSSA-external LSA: used in NSSA in place of type 5. used by ASBR
- Stub area: 
	- no external type 5 routes
	- replaced with default routes
	- wont accept routes from a different domain
	- redistribution is not allowed
- Totally stubby area:
	- no external type 5 or inter area type 3 routes
	- replaced with default route
	- redistribution not allowed
- NSSA: not so stubby area
	- cisco proprietary
	- normal stub area, but redistribution is allowed
- totally NSSA:
	- cisco proprietary
	- like totally stubby area, but redistribution is allowed
- path selection:
	- based on cumulative cost in dest
	- cost is based on interface bandwidth
	- default reference bandwidth is 100 mbps, but can be changed
	- cost = reference bandwidth / interface bandwidth
- tie breaker: if there is a tie, then choose based on below
	- intra area: choose this first
	- inter area: then this
	- external: then this


# BGP
- exterior gateway protocol
- routering protocol of the internet
- TCP port 179
- path vector protocol
- exchange layer 3 reachability info with other peers
- AS numbers: 0-65535
	- 0 reserved
	- 1-64495: public AS numbers
	- 64496-64511: reserved to use in documentation
	- 64512-65534: private AS, for IGP
	- 65535: reserved
- Must get AS number from a regional internet registry, and they get them from IANA
- BGP table
	- list of prefixes known by bgp
	- prefixes shared to peers
	- add new routes from routing table
- network statements
	- must match an exact prefix
	- add/inject route to bgp table form routing table
	- doesn't interfere with neighbors like IGPs
	- no wildcard logic
- to advertise summary networks: use a null route to create exact match
- BGP neighborships
	- manually configured, not dynamicalled discovered
	- same AS number as iBGP
	- different AS number as eBGP
	- neighbor states
		- idle: neighbor not responding
		- active, attempting to connect
		- connect, TCP session is established
		- open sent, open message sent
		- open confirm, response received
		- established, adjacency established
	- need neighbor statements to form neighbor ship, peer must have mirror statement
- mutual redistribution: advertise routes learned form different sources on same router
	- when a router redistrbutes bgp into ospf and ospf into bgp
- eBGP: admin dist of 20, between routers in different AS
- iBGP: bgp peering in routers in same AS, admin distance of 200
	- must be in full mesh: every router needs to be connected to each other

# PAT
- PAT is translation ip addresses from private to public while minimizing public ip usage
- 

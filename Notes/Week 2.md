
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
- 


- 2 physical switches are treated as a single logical switch
- Management and control plane are centralized
- data plane is distributed

# Multi-Chassis EtherChannel (MEC)
- Also called Multi-Chassis Link Aggregation Group (MLAG)
- only possible when using switch stacking
- for a regular etherchannel on an access switch, but the access switch connects to 2 different chassis on the stacked distribution switch
- used so that STP does not block a port

# Virtual Switching System (VSS)
- only allows 2 switches to be stacked
- supported on catalyst 4500, 5500, 6500 switches
- Largely replaced by StackWise Virtual (modern catalyst 9000 switches) and vPC (nexus switches)
- Virtual Switch Link (VSL) - connects the two switches to form stack
	- comprised of at least 1, ideally more, high speed links (10g or 40g)
	- acts as the backbone, which carries control plane info and data plane traffic. also carries the traffic that maintains the VSS
- Virtual Switch Link Protocol (VSLP) - used to establish and maintain the VSL
	- comprised of 2 sub protocols: LMP and RRP
	- Link Management Protocol (LMP) - verifies that the links are up. Exchanges various other info
	- Role Resolution Protocol (RRP) - makes sure the hardware and software are compatible. determines which switch is active and passive. depending on the compatibility, 1 of 2 modes will be used
		- Route Processor Redundancy (RPR) - active switch is functioning. passive switch cannot forward traffic. If active switch fails, passive switch can forward data again, it also maintains control plane data
		- Nonstop forwarding/stateful switchover (NSF/SSO) - the good mode. both switches forward data. passive switch maintains copy of control plane info
# StackWise
- can have up to 8 or 9 switches stacked together
- uses stack ports to do the stacking. they are proprietary
	- each switch has 2 stack ports so that they can form a ring topology: s1 -> s2 -> s3 -> s1
	- the ring topology is for redundancy sake
- Stack Discovery Protocol (SDP) - sends broadcast through stack cables to determine stack topology
- Active Switch
	- the election is taken place after SDP is used
	- the highest priority, then the lowest MAC address is used to determine the active switch
	- does the management plane, control plane, routing protocols, etc
- Standby Switch
	- 2 minutes after the active switch is elected, the standby switch is elected
	- same election parameters as the active switch
	- maintains a copy of the state of the active router to provide quick failover
- If a new switch is plugged in, the election will NOT be held again

# StackWise Virtual
- only allows 2 switches to form a stack
- essentially a replacement for VSS
- Stackwise Virtual Link (SVL) - same purpose as VSL
- This is used because Stackwise cables are super short (no more than 1 meter), but Stackwise virtual can use fiber optic across hundreds of meters.
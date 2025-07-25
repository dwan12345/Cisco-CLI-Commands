# UplinkFast
- speed up recovery from direct uplink failures. uplinks point towards the root bridge, so the root port
- if the root port's link goes down, it allows the switch to immediately switch a nondesignated port to forwarding
	- this means that on switches with no nondesignated ports, having uplinkfast does not help
	- Without uplinkfast: the nondesginated port becomes the root port, then it goes to listening and learning before forwarding
	- with uplinkfast: the nondesignated port becomes the root port, immediately go to forwarding
	- uplink fast makes the switch's priority become 49152. this is because uplinkfast switches are not mean to ever be the root bridge
- how to turn it on. this should only be turned on on the switches that can use this
```js
! configures uplinkfast
conf t
spanning-tree uplinkfast
end
```

# BackboneFast
- speed up recovery from indirect link failures. indirect link failures are links that are not directly connected to the switch
- backbonefast allows the switch to skip the max age timer and immediately put a nondesignated port into the listening state after receiving an inferior BPDU from a neighbor
	- the scenario is that the neighbor's root port goes down, now the neighbor thinks it is the root bridge and starts broadcasting BPDUs. The backbonefast switch sees this, so it stops blocking its port and sends the actual root bridges BPDUs
	- the network will be down for 30 seconds instead of 50 seconds
	- when the inferior BPDU is received, the backbone fast switch sends out a Root Link Query (RLQ) to the root bridge to check if the root bridge is alive. The root bridge will reply with a RLQ response, once the backbonefast switch receives the response, it will immediately change its nondesignated port
- should be enabled on all switches in the LAN
```js
! configure backbonefast
conf t
spanning-tree backbonefast
end
```

# RSTP
- uplinkfast and backbonefast are incorporated by default
- there is a sync mechanism: to help the topology converge very fast
- if sync mechanism succeeds, move from discarding state immediately to forwarding state. If sync mechanism fails, then wait 15s to go to learning, then 15s to go to forwarding.
	- the sync mechanism will fail if RSTP connects to an STP
- Port Roles:
	- root: same
	- designated: same
	- alternate: alternate path to the root bridge. If root port goes down, this port immediately becomes the root port. there can be more than 1 alternate port per switch
	- backup: backup path to the same link as a designated port. only appears in hubs

# RSTP Sync Process
- the process that makes convergence pretty much instant for RSTP
- this process happens in less than a second:
	1. each switch thinks its the root bridge, they each send BPDUs with the proposal bit set.
	2. The inferior switch accepts the proposal and superior switch ignores the proposal. The port on the inferior switch becomes the root port.
	3. The inferior switch sends an agreement BPDU out of the root port, then immediately starts forwarding
	4. the superior switch receives the agreement BPDU, then immediately starts forwarding
- during the sync process, the inferior switch will block all downstream ports (ports that do not lead to the root bridge, its designated ports) so that loops are not created. They will only block for the duration of the sync process, which is less than a second.
- topology change - when a nonedge port enters the forwarding state
- when a topology change happens on the changed switch:
	1. changed switch will flush its MAC address table except for edge/portfast ports, then send TC flag BPDU out of its root port.
	2. another switch receives the TC flag BPDU, it will flush its MAC table the same way as above. then set the TC flag on all BPDUs it sends, which is out of the designated and root ports, except the port the original TC BPDU was received on.
	3. this propagates throughout the network.
	4. TC flag is only set for 2 * hello timer, the default is 4 seconds.













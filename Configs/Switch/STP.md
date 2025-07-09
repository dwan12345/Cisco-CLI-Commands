- Root bridge elected based on lowest priority, then lowest MAC address. The priority goes down by 4096 intervals
- Ports types:
	- root port: lowest cost to root bridge
	- designated port: a port in forwarding mode. every network segment has at least 1 designated port. 
	- blocked port: blocked port
	- In case of ties, choose the switch with the lower priority, then lower MAC address. In case it is the same switch, then choose the interface on the other end with the lower port priority, then lower port number
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

# RSTP
- Multiple Spanning Tree (MSTP) and Rapid PVST+
- Nominates root bridge, root ports, etc the same way as STP
- The only port states are Discarding, Learning, and Forwarding. 
- When a switch's port goes down, it immediately sends out BPDU and Topology Change (TC) bit set. The switch flushes its MAC address table and any switch receiving the TC BPDU flushes their table as well.
- If a switch misses 3 Hello Packets, it assumes the link is down and initiates convergence. Instead of about 20 seconds, it takes 6 seconds to initiate convergence
- Alternate Port: new port role. If the root port goes down, the alternate port immediately becomes root port. 
- Link types:
	- edge: to end host. Same thing as portfast. Does not go through the port states process
	- point to point: from switch to switch
	- Shared: only for links connected to hubs

## Configure STP Priority
- change primary to secondary to configure secondary root bridge
- Can do STP load balancing by configuring different root bridges for the vlans
```js
conf t
spanning-treevlan <vlan num> root primary
end
```

## Portfast and BPDU Guard Default
```js
! configures portfast and BPDU default
conf t
spanning-tree portfast default
spanning-tree portfast bpduguard default
end
```


## Disable Portfast and BPDU Guard
- If using those settings by default, disable on these interfaces: to other switches, to routers, routed interfaces, anything other than end hosts
```js
! disable portfast and BPDU guard
conf t
int [interface]
	no spanning-tree portfast
	no spanning-tree bpduguard
	end
```


## Enable Portfast and BPDU Guard on an Interface
```js
! enables portfast and BPDU guard on an interface
conf t
int <interface>
	spanning-tree portfast
	spanning-tree bpduguard enable
	end
```


# BPDU Filter
- Prevents a port from sending BPDUs. The port will also ignore nay BPDUs
- Generally avoided because it turns on STP on that port, meaning it can cause loops.
```js
!
conf t
int <interface>
	spanning-tree bpdufilter enable
	end
```

## Root Guard
- if switch received superior BPDU on an int, the switch will not accept the new switch as the root switch and disables the interface
```js
conf t
int <interface>
	spanning-tree guard root
	end
```


## Loop Guard
- If the interface stops receiving BPDUs, it will not start forwarding. This is for interfaces that break in only one direction from forming a loop
```js
conf t
int <interface>
	spanning-tree guard loop
	end
```


## Show
```js
show spanning-tree
show running | section spanning-tree
```
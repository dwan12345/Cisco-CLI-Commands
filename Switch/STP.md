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

## Enable Portfast and BPDU Guard on an Interface
```js
conf t
int <interface>
	spanning-tree portfast
	spanning-tree bpduguard enable
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
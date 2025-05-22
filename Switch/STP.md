
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
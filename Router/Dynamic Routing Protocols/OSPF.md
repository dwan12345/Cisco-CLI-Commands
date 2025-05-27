- Designated router (DR) - the router that connects with every other router. The other routers will grab the LSA table from this
- Backup designated router (BDR) - also connects with every other router, takes over DR role if DR ever goes down.
- Election of DR and BRD is based on:
	- Priority: higher wins. Default is 1. Set priority to 0 to make sure this router is not DR
	- Router ID: higher wins.
- LSA types:
	- Type 1: router LSA. contains info about directly connected routes. It is a self description. every router creates one and floods it to the area
	- Type 2: network LSA. Only from DR. Floods to area. It describes the network. This simplifies the LSDB and SPF algorithm.
	- Type 3: Summary LSA or inter-area LSA. Floods an entire area, a type 3 LSA from area 0 would flood area 1. Only from ABRs. Summarizes the area by advertising the network prefixes so that LSDBs in other areas are smaller.
## Basic Setup
```js
! sets up OSPF
conf t
router ospf <process id>
! add multiple network commands to advertise more networks
network <network address> <wildcard mask> area <area id>
end
```
## Advertise Default Route
```js
! advertise the default route
conf t
router ospf <process id>
default-info originate
end
```
## Reset OSPF Process
```js
clear ip ospf process
yes
```

## Passive Interface
```js
! configures OSPF
conf t
router ospf <process id>
passive-int <interface>
end
```

## Configure Router ID
```js
! configure the router id
conf t
router ospf <ospf process id>
router-id <router id ip address>
end
```

## Share Routes from BGP
```js
! advertises routes learned from BGP
conf t
router ospf <ospf process id>
redistribute bgp <AS number on this router> subnets
end
```


## Configure Metric Bandwidth
```js
! configure ospf metric speed
conf t
router ospf <process id>
auto-cost reference-bandwidth <bandwidth mbps>
end
```


## Configure OSPF Priority
- Done in interface config mod for some reason
```js
! configure the OSPF priority
conf t
int <interface>
	ip ospf priority <0-255>
	end
```

## Show
```js
show ip ospf
show ip ospf neighbor
show ip ospf int brief
show ip route ospf
show running-config | section ospf
! Show all known routes to ospf
show ip ospf rib
```









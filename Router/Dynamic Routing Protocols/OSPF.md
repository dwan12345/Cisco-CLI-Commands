- Timers:
	- Hello timers: how often router sends out hello message
	- dead timer: how long it takes for neighborship to expire, refreshed by hello message. It is always 4 times the hello timer. 
	- If hello and dead timer do not match, then a neighborship cannot form.
- Network type: serial connection is point-to-point connection while ethernet to a switch is a broadcast network. If the network interface does not match, then OSPF neighborship will not form.
- Designated router (DR) - the router that connects with every other router. The other routers will grab the LSA table from this
- Backup designated router (BDR) - also connects with every other router, takes over DR role if DR ever goes down.
- Election of DR and BRD is based on:
	- Priority: higher wins. Default is 1. Set priority to 0 to make sure this router is not DR
	- Router ID: higher wins.
- LSA types:
	- Type 1: router LSA. contains info about directly connected routes. It is a self description. every router creates one and floods it to the area
	- Type 2: network LSA. Only from DR. Floods to area. It describes the network. This simplifies the LSDB and SPF algorithm.
	- Type 3: Summary LSA or inter-area LSA. Floods an entire area, a type 3 LSA from area 0 would flood area 1. Only from ABRs. Summarizes the area by advertising the network prefixes so that LSDBs in other areas are smaller.
	- Type 4: ASBR summary LSA. Tells routers where the ASBR is.
	- Type 5: external LSA. From ASBRs. For advertising prefixes from other routing protocols. Floods through area. 
	- Type 7: NSSA LSA. Only from ASBR in NSSA areas. Exactly like type 5 LSAs, used for advertising external routes. 
- Area types:
	- Stub area: there is only 1 exit point, so knowing the exact routes is unnecessary. Type 4 and 5 LSAs are blocked, instead replaced by a default route to the ABR. 
	- Totally stubby area: cisco proprietary, more restrictive than stub area. Type 3, 4, 5 LSAs are blocked. Default route to ABR is injected.
	- Not so stubby area (NSSA): a stub area that is then connected to another AS that is running another routing protocol. The routers will use type 7 LSA to get the external routes to the other areas.
	- Totally NSSA: ????



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


## Add Prefix List
- already created prefix list
- Usually done at ABRs to filter out prefixes from one area to another
```js
! add a prefix list to OSPF
conf t
router ospf <ospf process ID>
area <area num> filter-list prefix <prefix list name> <in | out> 
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









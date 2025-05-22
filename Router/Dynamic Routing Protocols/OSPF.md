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
redistribute bgp <AS number on this router>
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

## Show
```js
show ip ospf
show ip ospf neighbor
show ip ospf int brief
show ip route ospf
show running-config | section ospf
show ip ospf rib
```








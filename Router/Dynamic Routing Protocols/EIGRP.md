
## Basic Setup
```js
! sets up EIGRP
conf t
router eigrp <eigrp AS number>
! add multiple network commands to advertise more networks
network <network address> <wildcard mask>
end
```
## Configure Router ID
```js
! configure the router id
conf t
router eigrp <locally significant AS number>
router-id <router id ip address>
end
```

## Advertise All Static Routes, Including Default
- the default-metric is used for default routes
```js
! advertise default route
conf t
router eigrp <locally significant AS number>
default-metric 10000 10 255 1 1500
redistribute static
end
```

## Share Routes from BGP
- for metric, use: metric 10000000 1 255 1 1500
```js
! advertise routes learned form bgp
conf t
ip eigrp <locally significant AS number>
redistribute bgp <BGP AS number> metric <bandwidth> <delay> <reliability> <load> <mtu>
end
```

## Share Routes from OSPF
```js
! share routes from OSPF
conf t
router eigrp <eigrp AS number>
redistribute ospf <ospf process ID>
end
```

## Passive Interface
- Interface does not send out hello messages and will not form neighbors, but this subnet is still advertised
```js
! form passive interface
conf t
router eigrp <eigrp AS num>
passive-int <interface>
end
```


## Show
```js
show ip eigrp neighbor
show ip eigrp topology
show ip route eigrp
show ip eigrp
show ip protocols
show ip eigrp interfaces
show running-config | section eigrp
```










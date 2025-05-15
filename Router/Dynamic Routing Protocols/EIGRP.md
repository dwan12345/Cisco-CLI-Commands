
## Basic Setup
```js
! sets up EIGRP
conf t
router eigrp <locally significant AS number>
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
```js
! advertise default route
conf t
router eigrp <locally significant AS number>
redistribute static
end
```

## Share Routes from BGP
```js
! advertise routes learned form bgp
conf t
ip eigrp <locally significant AS number>
redistribute bgp <BGP AS number>
end
```


## Show
```js
show ip eigrp neighbor
show ip route eigrp
show ip eigrp
show running-config | section eigrp
```










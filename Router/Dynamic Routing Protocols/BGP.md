## Basic Setup
```js
! enables bgp routing
conf t
ip bgp <AS number>
end
```

## Creates BGP Neighbor
```js
! creates BGP neighbor
conf t
ip bgp <AS number>
neighbor <neighbor ip> remote-as <neighbor AS number>
end
```

## Advertise a Network
```js
! advertise bgp network
conf t
ip bgp <AS number>
network <network IP> mask <subnet mask>
end
```

## Advertise OSPF Routes
```js
! advertise ospf routes to bgp neighbors
conf t
ip bgp <AS number>
redistribute ospf <ospf process id>
end
```

## Advertise EIGRP Routes
```js
! advertise eigrp routes to bgp neighbors
conf t
ip bgp <AS number>
redistribute eigrp <eigrp AS number>
end
```

## Configure BGP Router ID
```js
! configures BGP router ID
conf t
ip bgp <AS number>
bgp router-id <router ID>
end
```


## Show
```js
show ip bgp summary
show ip bgp neighbors
show running | section bgp
```





















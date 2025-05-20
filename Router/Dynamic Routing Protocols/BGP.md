## Basic Setup
```js
! enables bgp routing
conf t
router bgp <AS number>
end
```

## Creates BGP Neighbor
- soft-reconfig inbound makes it so you do not have to clear ip bgp for reconfigurations to take effect immediately
```js
! creates BGP neighbor
conf t
router bgp <AS number>
neighbor <neighbor ip> remote-as <neighbor AS number>
neighbor <neighbor ip> soft-reconfiguration inbound
end
```

## Advertise a Network
```js
! advertise bgp network
conf t
router bgp <AS number>
network <network IP> mask <subnet mask>
end
```

## Advertise OSPF Routes
```js
! advertise ospf routes to bgp neighbors
conf t
router bgp <AS number>
redistribute ospf <ospf process id>
end
```

## Advertise EIGRP Routes
```js
! advertise eigrp routes to bgp neighbors
conf t
router bgp <AS number>
redistribute eigrp <eigrp AS number>
end
```

## Configure BGP Router ID
```js
! configures BGP router ID
conf t
router bgp <AS number>
bgp router-id <router ID>
end
```


## Apply Route Map
```js
! applies a route map
conf t
router bgp <AS number>
neighbor <neighbors interface ip> route-map <route map name> <in | out>
end
```

## Reset BGP
- Clears the current BGP connections. The router will attempt to form neighborships again.
- To be done after altering BGP configs
- Will make the connection go down
```js
! clears the bgp connection
clear ip bgp <neighbors interface ip>
```

## Remote Neighborship
- need to configure this on both routers to work
- router needs a route to the neighbor ip for bgp to form neighborship
```js
! forms remote neighborship
conf t
router bgp <AS number>
neighbor <neighbor ip> remote-as <neighbor AS number>
neighbor <neighbor ip> ebgp-multihop <max # of hops you allow>
end
```
## Show
```js
show ip bgp summary
show ip bgp neighbors
show running | section bgp
show ip bgp neighbor <neighbor ip> advertised-routes (self explanatory)
show ip bgp neighbor <neighbor ip> routes (shows filtered routes)
show ip bgp neighbor <neighbor ip> received-routes (shows all routes received)
```




















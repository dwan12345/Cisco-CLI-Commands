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
- For BGP to advertise a route, the network command must have an exact match for the route already in the routing table
- the static route to null0 creates the exact match in the routing table, which allows bgp to advertise the route. More specific routes will work fine, but routes that do not exist will get caught by the null0 and will disappear
```js
! advertise bgp network
conf t
router bgp <AS number>
network <network IP> mask <subnet mask>
exit
ip route <network IP> <subnet mask> null0
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

## Clear BGP
- soft reset will not tear the entire adjacency down, but will redo the routes
```js
clear ip bgp * soft
```

## Show
```js
show ip bgp
show ip bgp summary
show ip bgp neighbors
show running | section bgp
show ip bgp neighbor <neighbor ip> advertised-routes (self explanatory)
show ip bgp neighbor <neighbor ip> routes (shows filtered routes)
show ip bgp neighbor <neighbor ip> received-routes (shows all routes received)
```

















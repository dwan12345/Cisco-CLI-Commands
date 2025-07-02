
## Route Map
- Configure prefix list before hand
- Can change the sequence number on the same route map name to add more rules
- Example use: prefix list permits 1.1.1.1/32 and 2.2.2.2/32, route map says deny matches to this prefix list, so deny 1.1.1.1 and 2.2.2.2.
```js
! creates a route map
conf t
route-map <route map name> <permit | deny> <sequence num> 
match ip address prefix-list <prefix list name>
end
```


## Prefix List
- watch this if you do not understand le, ge: https://www.youtube.com/watch?v=qVNqB8o2EFs
- Add more sequence numbers to make more complicated list
```js
! configures a prefix list
conf t
ip prefix-list <prefix list name> seq <sequence num> <permit | deny> <ip/cidr>
!ip prefix-list <prefix list name> seq <sequence num> <permit | deny> <ip/cidr> <le | ge> <min/max prefix length to be matched>
end
```


## Show
```js
show ip prefix-list
show route-map
```






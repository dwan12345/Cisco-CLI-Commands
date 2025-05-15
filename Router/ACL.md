
## Define Extended ACL
```js
! define an extended ACL
conf t
ip access-list extended <ACL name>
end
```
## Add Rules to Extended ACL
- Replace protocol with: tcp, udp, ip, icmp, etc.
- Can replace IP and wildcard mask with "any"
- Replace operator with: eq, gt, lt, neq (not equal), range
```js
! add rules to extended ACL
conf t
ip access-list extended <ACL name>
<permit | deny> <protocol> <source ip> <source wildcard mask> <dest ip> <dest windcard mask> <operator> <port number>
end
```
## Apply ACL to Interface
- to the same port, can apply 1 ACL in, and 1 ACL out.
```js
! apply ACL to a port
conf t
int <interface>
ip access-group <ACL name> <in | out>
end
```
## Define Standard ACL
```js
! creates a standard ACL
conf t
ip access-list standard <ACL name>
end
```

## Add Rules to Standard ACL
```js
! add rules to standard ACL
conf t
access-list <ACL name> <permit | deny> <source ip> <wildcard mask>
end
```


## Show
```js
show ip access-lists
show running | section access-lists
show running | include ip access-group
```



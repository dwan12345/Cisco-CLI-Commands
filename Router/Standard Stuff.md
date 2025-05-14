
## Basic Interface
```js
! standard routed interface
conf t
int <interface>
desc <description>
ip address <ip address> <subnet mask>
shut
no shut
end
```

## Static Route
```js
! creates a static route
conf t
ip route <dest network address> <subnet mask> <next hop ip address>
end
```












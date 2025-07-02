
## SVI
```js
! creates an SVI
! create the vlan first
conf t
int vlan <vlan#>
desc <description>
ip address <default gateway ip> <subnet mask>
shut
no shut
end
```

## Loopback Address
```js
! loopback address
conf t
int loopback <loopback number>
ip address <ip address> 255.255.255.255
desc <description>
end
```

## Routed Interface
```js
! normal routed interface
conf t
int <interface>
no switchport
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






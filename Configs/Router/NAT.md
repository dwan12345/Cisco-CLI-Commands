## Set Inside and Outside Interfaces
- do this on loopback interfaces as well
```js
! sets the inside and outside interfaces
conf t
int range <inside interface range>
ip nat inside
int range <outside interface range>
ip nat outside
end
```

## Configure a Pool
 - cannot use network/broadcast IP for the IPs below
 - If public IP is /32, then use the single public IP for both first IP and second IP
 - first IP does not have to be first usable IP, second IP does not have to be last usable IP, this is just the norm. You can create multiple pools.
```js
! creates a pool for NAT
conf t
ip nat pool <pool name> <first ip> <second ip> netmask <subnet mask>
end
```

## PAT 
- Must have created a pool and ACL before configuring this
```js
! configures PAT with a pool
conf t
ip nat inside source list <ACL name> pool <pool name> overload
end
```

## PAT using an Interface Instead of a Pool
```js
! configures PAT with an interface
conf t
ip nat inside source list <ACL name> int <interface> overload
end
```

## Dynamic NAT
- Must have created a pool and ACL before configuring this
- 1 to 1 mapping from a pool of public IP addresses
```js
! configures dynamic NAT
conf t
ip nat inside source list <ACL name> pool <pool name>
end
```

## Clear Dynamic NAT Translations
- does not clear static NAT
```js
!clears dynamic NAT translations
clear ip nat translations *
```

## Static NAT
- 1 to 1 mapping
```js
! configures static NAT
conf t
ip nat inside source static <private ip> <routable ip>
end
```

## Show
```js
show ip nat translations
show ip nat statistics
```

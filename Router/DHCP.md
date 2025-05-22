

## Reserve IP Addresses
```js
! reserve from IP addresses from being used in DHCP
conf t
ip dhcp excluded-address <first ip> <last ip>
end
```


## Configure Router as DHCP Server
- should create separate DHCP pool for each subnet
- DNS server can be 8.8.8.8, Google's DNS
- domain name is optional
```js
! makes this router act as dhcp server
conf t
ip dhcp pool <pool name>
	network <ip> <cidr>
	dns-server <dns server ip>
	! domain-name <name of domain>
	default-router <default gateway ip>
	lease <days> <hours> <minutes>
	end
```

## Relay Agent
- interface is usually the default gateway or whichever interface that will receive DHCP relay messages
```js
! configures relay agent on a port
conf t
int <interface>
	ip helper-address <ip of dhcp server>
	end
```

## Router Get IP From DHCP
- not sure why you would do this
```js
! get interface IP from dhcp
conf t
int <interface>
	ip address dhcp
	end
```

## Show
```js
show running | i dhcp
show running | i helper
show running int <interface>
show ip dhcp binding
```






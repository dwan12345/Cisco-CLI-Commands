- DHCP Message Types
	- Discover: client broadcast in local network to check for DHCP server
	- DHCP Offer: unicast to MAC address of client, destination IP is IP address being offered. 
	- Request: Client sent to server, broadcast, will contain the IP of the DHCP server
	- Ack: server to client, server tells client it is ok to use the IP. Dest IP is IP being offered. Unicast. 
	- Release: from client to server, unicast, release the IP of the client.

## Reserve IP Addresses
```js
! reserve from IP addresses from being used in DHCP
conf t
ip dhcp excluded-address [first ip] [last ip]
end
```


## Configure Router as DHCP Server
- should create separate DHCP pool for each subnet
- DNS server can be 8.8.8.8, Google's DNS
- domain name is optional
```js
! makes this router act as dhcp server
conf t
service dhcp
ip dhcp pool [pool name]
	network [ip] [cidr]
	dns-server [dns server ip]
	! domain-name [name of domain]
	default-router [default gateway ip]
	lease [days] [hours] [minutes]
	end
```

## Relay Agent
- interface is usually the default gateway or whichever interface that will receive DHCP relay messages
```js
! configures relay agent on a port
conf t
int [interface]
	ip helper-address [ip of dhcp server]
	end
```

## Router Get IP for an Interface From DHCP
- not sure why you would do this
```js
! get interface IP from dhcp
conf t
int [interface]
	ip address dhcp
	end
```


## DHCP Snooping
- Trusted ports should always face the DHCP server, while every other port should be untrusted. By default, all ports are untrusted
- Any server DHCP messages received on untrusted port, it is dropped
- If client DHCP messages received on untrusted port, it is inspected and either dropped or forwarded. 
	- For example, for release messages, check the DHCP snooping binding table to check if IP, MAC addresses, and interfaces match the release message
- Trusted port is always forwarded
```js
! enable dhcp snooping
conf t
ip dhcp snooping
ip dhcp snopping vlan [vlan num]
no ip dhcp snooping information option
end
```

```js
! dhcp snooping, trust a port
conf t
int [interface] 
ip dhcp snooping trust
end
```
- DHCP snooping rate limiting can limit how many DHCP messages hit an interface, if over, then it disables it
```js
! dhcp snooping rate limiting
conf t
int [interface]
ip dhcp snooping limit rate [how many per sec]
end
```


## Show
```js
show running | i dhcp
show running | i helper
show running int <interface>
show ip dhcp binding
show ip dhcp pool
show ip helper-address
! to see the dhcp snooping binding table
show ip dhcp snooping trust
```






- The first 64 bits are network address, the last 64 bits are host address
	- Global routing prefix: the first 48 bits. Assigned by the ISP, like a public internet address. 
	- Subnet Identifier: the last 16 bits of the network address. Used by enterprises for subnetting.
	- Interface identifier: the last 64 bits. For the hosts. 
- EUI64 (Extended Unique Identifier): convert 48 bit mac address to 64 bit interface ID. This 64 bit ID is then used for the host port of the ipv6 address
	- To create: insert FFFE right in the middle of the mac address, then invert the seventh bit
		- mac address: 1234 5678 90AB converts to EUI64: 1034 56FF FE78 90AB
	- Apparently, it is not used for a while now due to privacy concerns
```js
! to configure an interface using eui-64
int <interface>
ipv6 address <ipv6 network address /cidr> eui-64
```
- Address types
	- Global unicast: globally unique global addresses. Range is 2000::/3
	- Unique local: private addresses that cant be used on the internet. Range is FD00::/7
	- Link local: used for communication within a single subnet. automatically generated on ipv6 enabled interfaces. FE80::/10. The next 54 bits are all 0s, the last 64 bits are EUI64
	- Multicast: FF00::/8. 
	- Anycast: hits the first 1 that matches the group. No address range, any unicast address can be treated as anycast group. Below, there are 2 "ip address" commands, they will both be added to the interface. 
```js
int <interface>
ipv6 address <ipv6 address /cidr>
ipv6 address <ipv6 address /cidr> anycast
```
- Unspecified address: when devices no do know their ipv6, also used to reference default routes. ::/0
- loopback: used to test the protocol stack on the device. ::1. The ipv4 equivalent is 127.0.0.0/8.

## Multicast Addresses
- Address scopes:
	- FF01: interface local, does not leave the local device
	- FF02: link local, within the subnet, dropped by routers
	- FF05: site local, can be forwarded by routers, but should be within single physical location
	- FF08: organization local, wider in scope than site local
	- FF0E: global, no boundaries, can be sent over the internet
- Multicast Address Groups:
	- FF0X::1 - all nodes, broadcast (ipv4 equivalent: 224.0.0.1)
	- FF0X::2 - all routers (ipv4 equivalent: 224.0.0.2)
	- FF0X::5 - all OSPF routers (ipv4 equivalent: 224.0.0.5)
	- FF0X::6 - all OSPF DR and BDRs (ipv4 equivalent: 224.0.0.6)
	- FF0X::9 - all RIP routers (ipv4 equivalent: 224.0.0.9)
	- FF0X::A - all EIGRP routers (ipv4 equivalent: 224.0.0.10)

## Network Discovery Protocol (NDP)
- Replaces ARP for ipv6 using multicasts
- RS (router solicitation): when host connects to network, they send out RS messages to multicast FF02::2, which will reach all routers on the local subnet
- RA (router advertisement): routers will respond to RS with RA. Routers will occasionally send out RAs. They are sent to FF02::1. It contains info such as router ipv6 address, whether to use SLAAC, etc.
- NS (neighbor solicitation): destination IP address is the "solicited node multicast address," which is derived from the destination ipv6 address.
- NA (neighbor advertisement): a host will respond to NS with its mac address.

## SLAAC
- stateless address auto configuration
- is turned on by default
- a host will use RS and RA to learn the prefix of the local subnet, and then automatically generates an ipv6 address for itself (either randomly or using EUI64).
- It uses DAD (Duplicate Address Detection) to check for duplicate addresses.
	- Uses NS on its own ipv6 and then checking on the NAs to see if there is another host with the same ipv6 on the subnet
	- This is always performed upon configuring the ipv6 on an interface


## Basic Configuration
```js
! enables ipv6
conf t
ipv6 unicast-routing

! assign ipv6 to interface
int <interface>
ipv6 address <ipv6 address /cidr>
no shut
exit
```

## Show
```js
show ipv6 int br
```



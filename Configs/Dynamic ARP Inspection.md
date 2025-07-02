- Defend against ARP poisoning (gratuitous ARP), 
- all ports are untrusted by default
- Generally, ports connected to end hosts are untrusted while ports connected to switches and routers are trusted
- Inspects ARP messages on untrusted ports, and either drops and forwards it
	- checks sender MAC, sender IP, interfaces against the DHCP snooping binding table
```js 
! enable dynamic arp inspection and trust some ports
conf t
ip arp inspection vlan [vlan num]
int range [interface range]
ip arp inspection trust
end
```
- rate limiting is configured on the receiving interface
```js
! configure dynamic arp inspection rate limiting
conf t
int range [interface range]
ip arp inspection limit rate [num] {burst interval [seconds]}
end
```
- Additional checks: must state multiple validation commands to use multiple of them
	- dst-mac: check destination MAC of the frame against the destination MAC of the ARP message
	- ip: checks for invalid IP addresses such as 0.0.0.0
	- src-mac: check source MAC of the frame against the source MAC of the ARP message
```js
! configure additional dynamic arp inspection validation checks
conf t
ip arp inspection validate [dst-mac | ip | src-mac] {dst-mac | ip | src-mac}
end
```



## Show
```js
show ip arp inspection {interfaces}
```














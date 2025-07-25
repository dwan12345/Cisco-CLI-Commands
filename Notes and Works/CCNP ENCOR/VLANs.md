- stretched VLANs - VLANs that are spread out across multiple sites
- internal vlan - on a L3 switch, when you created a router interface, it creates an internal vlan exclusively used for that link.
	- this vlan will not appear in show vlan
	- this vlan cannot be created to be used elsewhere
	- to use this vlan, you have to shutdown the link

# Multiple Subnets per VLAN
- you can have multiple subnets for 1 vlan, ie: 10.0.0.0/24 and 10.0.67.0/24 for vlan 10
- do this by using secondary IP address
- for SVIs
```js
conf t
int vlan <vlan num>
ip address <ip> <subnet mask> secondary
end
```
- for router on a stick
```js
conf t
int <interface>.<vlan num>
ip address <ip> <subnet mask> secondary
end
```

# Commands
- shutdown a vlan, the switch will not switch for that vlan
```js
conf t
vlan <vlan num>
shutdown
end
```


## On Bootup
```js
enable
conf t
enable secret <password>
username <username> secret <password>

! for local management
line con 0
logging synchronous
login local
exit

! for remote management
line vty 0 4
logging synchronous
login local
exit

hostname <hostname>

! only for layer 2 switches
(no ip routing)
end
```


## Creating Vlans
```js
conf t
vlan <vlan#>
name <name>
end
```


## Management Vlan Interface
```js
conf t
vlan <vlan#>
name <name>
exit
int vlan <vlan#>
desc <Management interface name>
ip address <ip address> <subnet mask>
shut
no shut
end
```





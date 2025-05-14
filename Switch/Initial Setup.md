	
## On Bootup
```js
! initial setup
enable
conf t
enable secret <password>
username <username> secret <password>
line con 0
logging synchronous
login local
exit
line vty 0 4
logging synchronous
login local
exit
hostname <hostname>

! keep 1 of 2 below, will mess with management vlan if configured wrong
(no ip routing)
(ip routing)
end
```


## Creating Vlans
```js
! creating vlans
conf t
vlan <vlan#>
name <name>
end
```


## Management Vlan Interface
```js
! vlan management interface
conf t
vlan <vlan#>
name <name>
exit

conf t
int vlan <vlan#>
desc <Management interface name>
ip address <ip address> <subnet mask>
shut
no shut
end
```





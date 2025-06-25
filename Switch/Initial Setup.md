	
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


## SVI
- Make the VLan first
```js
! Creates SVI
conf t
int vlan <vlan#>
desc <Management interface name>
ip address <ip address> <subnet mask>
shut
no shut
ip default-gateway <default gateway of management vlan>
end
```





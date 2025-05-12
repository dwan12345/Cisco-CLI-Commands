
enable
conf t
enable secret cisco
username cisco secret cisco

! for local management
line con 0
logging synchronous
login local
exit

! for remote management
line yty 0 4
logging synchronous
login local
exit


hostname wgsCA67a02a01


no ip routing


vlan 1671
name USERS1
exit

vlan 2671
name USERS2
exit


int vlan 1671 
desc RMT_MGMT
ip address 10.2.67.14 255.255.255.248
shut
no shut
exit


int g0/2
desc to_james
switchport mode access
switchport access vlan 1671
shut
no shut
exit


int g0/1
desc to_RTRCA
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan 1671,2671
shut
no shut
exit


write mem









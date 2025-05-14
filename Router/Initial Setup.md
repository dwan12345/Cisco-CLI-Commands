
## On Bootup
```js
! initial router setup
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
end
```

## Loopback Address
```js
! loopback address
conf t
int loopback <loopback number>
ip address <ip address> 255.255.255.255
desc <description or MGMT>
end
```
















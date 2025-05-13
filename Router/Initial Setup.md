
## On Bootup
```js
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


















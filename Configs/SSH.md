
# SSH
- these configurations are the prerequisites to use SSH for the VTY lines.
```js
! 
conf t
hostname <hostname>
ip domain name <domain name>
crypto key generate rsa modulus 2048
end
```
# VTY Lines
- VTY lines are what is used for remote connection
- there are a total of 16 lines, meaning 16 people can manage it at the same time.
- "line vty 0 15" means to configure all of the lines, you can do "0 7" to configure line 0 to 7
- "transport input" have way more options, you can do "transport input telnet ssh" to allow multiple protocols
```js
conf t
enable secret <pw>
username <username> secret <pw>
line vty 0 15
login local
transport input <all | telnet | ssh>
[exec-timeout 5 0]
[access-class <acl name> in] 
```


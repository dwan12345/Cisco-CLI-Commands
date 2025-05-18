
## Relay Agent
```js
! configures relay agent on a port
conf t
int <interface>
ip helper-address <ip of dhcp server>
end
```


## Show
```js
show running | i dhcp
show running | i helper
show running int <interface>
```






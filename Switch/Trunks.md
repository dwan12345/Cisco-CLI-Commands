

## Setting up a trunk on an interface
```js
! already in escalated mode
conf t
int <interface>
switchport mode trunk
switchport trunk allowed vlan <vlan#>,<vlan#>
end

```



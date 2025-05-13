

## Setting up a trunk on an interface
```js
conf t
int <interface>
desc <description>
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan <vlan#>,<vlan#>
end

```



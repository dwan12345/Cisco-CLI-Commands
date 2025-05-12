
```
conf t
int <interface>
no shutdown

! repeat next section for however many subinterfaces
int <interface>.<vlan#>
encapsulation dot1q <vlan#>
ip address <default gateway of subnet> <subnet mask>

end

```






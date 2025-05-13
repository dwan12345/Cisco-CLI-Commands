
```js
conf t
int <interface>
shut
no shut

! repeat next section for however many subinterfaces
int <interface>.<vlan#>
desc <description>
encapsulation dot1q <vlan#>
ip address <default gateway of subnet> <subnet mask>

end
```






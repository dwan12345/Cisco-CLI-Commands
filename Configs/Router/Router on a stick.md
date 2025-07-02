
```js
! sets up router on a stick
conf t
int <interface>
desciption <description or subinterfaces_from_switch>
no ip address
shut
no shut
! repeat next section for however many subinterfaces
int <interface>.<vlan#>
desc <description or vlan#_default_gateway>
encapsulation dot1q <vlan#>
ip address <default gateway of subnet> <subnet mask>
shut
no shut
! end of section
end
```


## Show
```js
show run interface <interface>.<vlan#>
```



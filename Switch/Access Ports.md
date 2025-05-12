
## Basic setup
```js
conf t
int range <interface range> 
desc <desciption>
switchport mode access

! delete this line if not setting vlan
switchport access vlan <vlan#> 

shut
no shut
end

```







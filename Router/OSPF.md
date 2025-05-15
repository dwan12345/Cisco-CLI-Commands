

## Basic Setup
```js
! sets up OSPF
conf t
router ospf <process id>
! add multiple network commands to advertise more networks
network <network address> <wildcard mask> area <area id>
end
```

## Advertise Default Route
```js
! advertise the default route
conf t
router ospf <process id>
default-info originate
end
```


## Reset OSPF Process
```js
clear ip ospf process
yes
```

## Configure Router ID
```js
! configure the router id
conf t
router ospf <ospf process id>
router-id <router id ip address>
end
```













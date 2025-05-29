
## HSRP
- Good practice to match group number to vlan
- switches to HSRP v2
- The priority number (default is 100) is used to determine which router will be the active router.
	- Active router will be highest priority, then highest IP address
- optional prempt in there
```js
! sets up HSRP
conf t
int <default gateway>
standby version 2
standby <group number> ip <virtual IP>
standby <group number> priority <priority number>
! standby <group number> preempt
! stanby <group number> preempt delay <seconds>
end
```


## Show
```js
show standby
show standby int <interface>
show standby group <group number>
show standby brief
```











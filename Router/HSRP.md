
## Basic Setup
- Good practice to match group number to vlan
- The priority number (default is 100) is used to determine which router will be the active router.
	- Active router will be highest priority, then highest IP address
```js
! sets up HSRP
conf t
int <interface>
standby <group number> ip <virtual IP>
standby <group number> priority <priority number>
end
```

## Change to HSRP v2
```js
! change interface to HSRP v2
conf t
int <interface>
standby version 2
end
```


## Activate Preemption
- When in preempt, a higher priority router will take active router role forcefully.
```js
! activates preemption for HSRP
conf t
int <interface>
stanby <group number> preempt
end
```















## Configure Port Security
- maximum: how many different MAC addresses are allowed
- violation: choose the violation mode
	- protect: drop bad frames, does not disable port, creates syslog message
	- restrict: drop bad frames, does not disable port, creates syslog message
	- shutdown: default, port is disabled, creates syslog message.
- mac-address: statically specify the mac address
- mac-address sticky: the first mac address learned is now added to the running config, meaning it essentially becomes a statically configured mac address. Since it is only added to running config, must save the config for it to save. 
```js
! port security stuff
conf t
int <interface>
	switchport mode <access | trunk>
	switchport port-security
	! switchport port-security maximum <num>
	! switchport port-security violation <protect | restrict | shutdown>
	! switchport port-security mac-address <mac address>
	! switchport port-security mac-address sticky
	end
```

## MAC Address Aging
- How long a dynamically learned mac address is kept before having to learn a new one. Statically configured mac addresses never age out
- Aging type
	- Absolute: default. does not refresh the aging time upon receiving a valid frame again
	- Inactivity: does refresh the aging time upon receiving a valid frame again
- Aging static: makes it so that static mac addresses also age out. Does not apply to sticky MAC addresses.
```js
! port security mac address aging stuff
conf t
int <interface>
switchport port-security aging time <minutes>
switchport port-security aging type <absolute | inactivity>
! switchport port-security aging static
end
```

## Show
```js
show port-security int <interface>
show mac address-table secure
show errdisable recovery
```
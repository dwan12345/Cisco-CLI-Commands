


## Configure Port Security
```js
conf t
int <interface>
	switchport mode <access | trunk>
	switchport port-security
	end
```


## Show
```js
show port-security int <interface>
```
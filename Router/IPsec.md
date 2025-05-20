
## GRE Tunnel
- Source tunnel ip is is private IP with /30, like 2 routers connected to each other.
- real world destination ip must be a real routable ip with an actual destination in the real world
- interface is the interface to leave out of to reach the end of the tunnel
- the square brackets are for attaching an IPsec profile
```js
! creates GRE tunnel
conf t
int tunnel <any number>
ip address <source tunnel ip> <subnet>
tunnel source <interface that leads to destination>
tunnel destination <real world destination ip>
[
tunnel mode ipsec ipv4
tunnel protection ipsec profile <profile name>
]
shut
no shut
end
```

## Set Up IPsec Aston Way
```js
! sets up the ipsec profile
conf t
crypto isakmp policy 1
	encryption aes
	authentication pre-share
	group 16
exit 
crypto isakmp key <password> address <peer ip>
crypto ipsec transform-set <transform set name> esp-aes esp-sha512-hmac
	mode tunnel
crypto ipsec profile <profile name>
	set transform-set <transform set name>
end
```


## Set Up IPsec YouTube Way
1. Create IKE policy
	- Lower priority will be used first. When routers first try IPsec, they will try to set up isakmp. They go down their isakmp policies until a compatible one is found with the other side, like ACL. 
```js
conf t
crypto isakmp policy <priority num>
autentication pre-share 
encryption aes
hash sha 
group 16
end
```
2. Define pre-share key
	- the ip means the router will use this password when setting up IPsec to this ip
	- remote peer ip can be replaced with ip and subnet mask to make router use this pw for a range of addresses
```js
conf t
crypto isakmp key <password> address <remote peer ip>
end
```
3. Create transform set. Defines how the data is protected.
	- AES used for encryption, SHA used for hashing
```js
conf t
crypto ipsec transform-set <transform set name, does not matter> esp-aes esp-sha-hmc
end
```
4. Define what is allowed.
	- "gre" only allows GRE traffic
	- can replace "any any" with whatever you want
```js
conf t
ip access-list extended <ACL name> 
permit gre any any
end
```
5. Putting previous steps into a container (crypto map).
	- "peer ip routable" is not the ip at the end of GRE tunnel, but the actual ip to get to the other router
```js
conf t
crypto map <any name> <any seq num> ipsec-isakmp
set peer <peer ip routable>
set transform-set <tramsform set name>
match address <ACL name>
end
```
6. Apply crypto map to interface
	- "interface" is not the tunnel interface, but the interface that leads towards the other end of the tunnel
```js
conf t
int <interface>
crypto map <crypto map name>
end
```

## Update Tunnel Bandwidth
- bandwidth should match on both ends
```js
! updates tunnel bandwidth
conf t
int tunnel <tunnel number>
bandwidth <num in kbps>
end
```

## Show
```js
show int tunnel <tunnel number>
show run | sec ipsec
show crypto isakmp sa
show crypto ipsec sa
```






- monitors the network by constantly simulating traffic, such as pings
## Set Up IP SLA
- frequency (5) is how often to send out pings, timeout (2000) is timeout, threshold (500) is if exceed -> triggers reaction even.
```js
conf t
ip sla <operation num>
	icmp-echo <dest ip> [source-ip <source ip> | source-int <int>]
		frequency <seconds>
		timeout <ms>
		threshold <ms>
		exit
ip sla schedule <operation num> start-time now life forever
end
```


## Track Object
- used for static route failover
```js
conf t
track <track num> ip sla <operation num> reachability
end
```


## Automatic Static Route Failover
```js
! use floating static routers and IP SLA
conf t
ip route 0.0.0.0 0.0.0.0 <main gateway> track 1
ip route 0.0.0.0 0.0.0.0 <backup gateway> 10
end
```


## Show
```js
show ip sla summary
show ip sla statistics
show track
```





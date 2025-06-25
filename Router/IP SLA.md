- monitors the network by constantly simulating traffic, such as pings

conf t
ip sla 1
icmp-echo 8.8.8.8
timeout 2000
threshold 500
frequency 5
exit
ip sla schedule 1 start-time now life forever
track 1 ip sla 1 reachability
no ip route 0.0.0.0 0.0.0.0 76.113.49.1
ip route 0.0.0.0 0.0.0.0 76.113.49.1 track 1
ip route 0.0.0.0 0.0.0.0 91.33.56.1 10 


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
conf t
ip route 0.0.0.0 0.0.0.0 <main gateway> track 1
ip route 0.0.0.0 0.0.0.0 <backup gateway> 10
```


## Show
```js
show ip sla summary
show ip sla statistics
show track
```





- works by sending packets with TTL of 1, then 2, then 3, etc. Each router will respond back with time exceeded ICMP messages, which will be analyzed by traceroute
- in the hostname section, the PC will attempt to reverse resolve the IP via its DNS server
- We see "destination unreachable" or "port unreachable" when using trace route in cisco IOS because cisco IOS uses random UDP ports. This means that the device is reachable and good. 
- Windows sends ICMP echo requests, all other OSs send UDP
- traceroute can give inaccurate info because many reasons:
	- load balanced: TTL 2 messages can take a different path in the network than TTL 3, making the path drawn from the traceroute be inconsistent
	- firewalls or routers refuse ICMP messages
- to skip the DNS reverse resolve to speed up the trace route in cisco IOS:
```js
traceroute <ip> numeric
```
- to skip DNS in windows trace route:
```js
tracert -d <ip>
```



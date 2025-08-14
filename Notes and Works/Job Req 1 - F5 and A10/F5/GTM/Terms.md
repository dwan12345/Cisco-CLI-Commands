- Listeners - listens for the DNS traffic on a specific IP and port (usually 53) that is intended for the GTM
- Wide IP - a FQDN that you want the GTM to manage. Pretty much like an A or AAAA record. 
- Pool - a group of virtual servers. Associated with a single data center. The Wide IP chooses which pool/data center to tell the user to use, then the pool/data center load balances across its virtual servers.
- Virtual Server (GTM Context) - essentially a virtual server in the LTM
- Data Center - an object that represents a data center. This object contains the pools. You define the geographic characteristics of the data center.
- iQuery - how geographically different GTMs and LTMs communicate with each other. trust must be established between the devices
- Synchronization Group - group of GTMs that sync their configs and operate in HA
- Dynamic Load Balancing
	- Completion Rate - measured in number of connections that were opened, processed, and closed properly.
	- Round Trip Time (RTT) - lowest latency from a data center. Measured from the data center to the local DNS server of the client
	- Topology - goes to nearest data center
- DNS64 - helps IPv6 only clients communicate with IPv4 only servers by referring them to a NAT64 gateway
	1. client tries to resolve "example.com"
	2. DNS server cannot find IPv6 for the domain, but it can find IPv4
	3. DNS server prepends a well known prefix to the IPv4 of the server and returns it to the client. It will be an actual IPv6 address that is returned
	4. The client goes to the IPv6, which connects to a NAT64 gateway due to the prefix
	5. refer to NAT64
- NAT64 - a gateway that helps IPv6 only clients communicate with IPv4 only servers
	1. the gateway sees the IPv4 at the end along with the client's source IPv6
	2. gateway talks to the IPv4 server using its own IPv4 address while forwarding the client's traffic
	3. the response traffic is forwarded back to the client.
- DNSSEC - protects DNS by adding authenticity and integrity to DNS responses. 
	- example attacks: DNS spoofing and cache poisoning
	- the idea is that there is no built in security mechanism to DNS. Someone could easily intercept your DNS query and respond back. Or they could tamper with the DNS response
	- uses private key and public key system
	- when a client contacts any DNS server (root server, TLD, or authoritative), they always confirm that they are actually talking to them. Whenever they get a response, they confirm that the response has not been tampered with
- DNS Express - a secondary DNS server that works along side the primary DNS server (Microsoft). DNS express can handle extremely volume of the internet queries and improves latency
	- resilient against DDOS attacks
	- reduced attacked surface because our primary DNS is not accessible from the internet
	- DNSSEC acceleration
- ZoneRunner - the actual DNS server on the F5
- F5 DNS Resolver Cache and Forward Lookup Zone - configure this to have the F5 forward unknown DNS requests to other DNS servers, such as Google. This also caches it, so the performance increases
	- verify using statistics -> module statistics -> DNS -> cache. View the cache to see hits and misses
	- verify by using a client. use nslookup on something that is not in the cache. use the same command again, the second time will be nearly instant
- 
- 



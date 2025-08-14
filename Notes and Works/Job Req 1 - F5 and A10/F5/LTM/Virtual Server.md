- Virtual Server (VS) - the entry point for client connections. Must have a VIP and port for which it listens for traffic
	1. client makes request. They resolve our name to get the VIP of our VS.
	2. VS receives the traffic, then applies profiles, iRules, polices
		- SSL offloading profile
		- other profiles such as TCP, HTTP, persistence, oneconnect, etc.
		- security policies from WAF and AFM
		- iRules applied
	3. load balance traffic to pool
	4. respond back to client
- Secure NAT (SNAT) - when the F5 sends its traffic to the server, the traffic will have a source IP of the SNAT IP, this will make the server respond back to the SNAT IP. Now the F5 can respond back to the client. This prevents the server from responding directly to the client using its default gateway, otherwise the TCP connection will break because the client sees a different IP responding, and otherwise it is insecure.
	- completely irrelevant if the servers default gateway is the F5


- when the F5 forwards a client's traffic to a server, usually the source IP is the client's IP. This causes issues because if the server's default gateway is not the F5, then the server will forward the traffic out of NOT the F5, and when the client receives it back, it will not know where it came from
- to solve the issue, when the F5 forwards traffic to the server, SNAT replaces the source IP of the packet to the internal self IP of the F5. It will then translate it back when it forwards the response to the client
- SNAT Automap - the most common. uses the self IP on the vlan of the servers
- SNAT pool - the F5 uses many IPs for SNAT. useful for high connection environments when a single IP will run out of ports.
- To configure:
	1. local traffic -> virtual servers -> *click on your VS* -> properties
	2. find "source address translation", and change it to automap or SNAT. SNAT means SNAT pool.
	3. choose the SNAT pool if you are using SNAT pool.
- to create SNAT pool: local traffic -> address translation -> SNAT pool list -> create
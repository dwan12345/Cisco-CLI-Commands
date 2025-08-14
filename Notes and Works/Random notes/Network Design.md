
# Network Edge
- find out the business goals
	- will it grow?
	- are there mission critical applications or users?
	- how much downtime can we afford?
	- budget?
- internet circuits
	- do we need 99.99% uptime from our ISP, or just a normal broadband?
	- what type of handoff is it? fiber? RJ45?
	- where is the minimum point of entry?
	- for redundant ISPs, try to get circuits that operate at different PoP, and more path diversity. but this is often not possible
- BGP and Failover for multihomed environments
	- for backup ISP, prepend your own AS path to make the return traffic less likely to use the backup ISP. you can also advertise a smaller subnet on the primary ISP because the smaller subnet is preferred. 
	- use local preference to route internal traffic to the main ISP
	- if BGP is not available, use static routing. this is less flexible
	- if you have multiple data centers with default routes, and you are not using iBGP, it could cause issues
- DMZ
	- best to get dedicated DMZ switches for scalability and clear separation of responsibility
	- if not using dedicated DMZ switch, then you can make use of existing infrastructure. Maybe a port on the core switch with a dedicated VLAN. Maybe ports on a leaf switch in a spine/leaf topology.

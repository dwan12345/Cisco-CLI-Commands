
# Two Tier Design
- Access layer: where hosts connect to 
	- QoS things, security devices such as port security and Dynamic ARP Inspection
	- PoE for wireless APs
- Distribution layer: aggregates connections from access layer switches
	- connect to internet, WAN, etc
- Each distribution layer L3 switch connects to every other L3 switch. They should run HSRP and connect to multiple ISPs for redundancy
- Access layer L2 switches do not connect to each other, they only connect to distribution switches, they do not need to connect to every distribution layer switch, only a couple

# Three Tier Design
- Additional core layer: every distribution layer switch connects to every core layer switch.
	- only focused on switching speed, so no CPU intensive things such as QoS, port security, etc
	- Only layer 3, no STP

# Spine Leaf Architecture 
- also called CLOS, Cisco ACI (Application Centric Architecture)
- for data centers, 2 tier
- Every leaf switch is connected to every spine switch, but leaf switches do not connect to leaf switches, spines do not connect to spines.
- Hosts connect to leaf switches. 
- This provides consistent latency and bandwidth between the hosts.

# SOHO
- one device does router, switch, firewall, wireless AP, modem, 











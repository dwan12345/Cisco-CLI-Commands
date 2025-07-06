
what are networks consists of?:
- servers, switches, load balancers, cables, firewalls, etc.

OSI model
- vendors pick a layer to specialize
- bits, frames, packets, segments, data, data, data
- session: maintaining conversations, TCP handshake
- presentation: generalization of data, translating from binary to actual data, also encryption and decryption
- application: what the user interacts with

LAN
- devices in a local area. 

WAN
- connects between 2 LANs that are not in the same area. 

MAN
- Like a single wireless network that is publicly available in a large metropolitan area

Cables
- crossover - pc to pc, switch to switch, pc to router
- straight through - switch to a router, printer to switch, router to switch
- roll over, console cable - connect to switch to manage the switch, or manage router, etc.
- stacking cable - connect multiple switches to combine into a single logical switch
- single mode fiber - slower than multi mode, long distance, smaller core
- multimode fiber - shorter distance, higher throughput, larger core

Carrier sense multiple access, with collision detection
- When collision is detected, one device tells the other device that collision has happened, so both stop transmitting. both devices pick a random time to start transmitting again, so that they do not collide again.

Collision and broadcast domains
- hub: same collision and broadcast domain
- switch: separate collision, same broadcast
- router: separate collision and broadcast

MAC Address Table
- binds port to MAC address
- show mac address-table

ARP Table
- Binds mac address to ip address
- show ip arp

3 Basic Methods of Connecting Subnets
- router connected to 3 switches
- inter vlan routing using L3 switch
- router on a stick

# General Routing
- list of nex hop IPs for dest
- list of all networks a router knows about
	- route entry for each active int
	- rout entry for each subnet learned form all protocols
- origin code: how the route was learned.
- Admin Distance (trust) - lower number is better, determines the preference in a tie
- First thing router does when it receives packet: do I have this ip directly connected? If not, then check if I have a route
- longest match rule - send packet to route that has longest match
- static routes:
	- con: lack of scalability, redundancy, has human error, high administrative overhead (cost a lot of engineer time which means money)
	- pros: low cpu usage and a little bit more secure
- For static route to be valid: valid destination network address, valid subnet, next hope ip must be accessible
- Static route optional params: name, admin distance
- ip route _destination network ip_ _subnet mask_ _admin distance_ 
- ip route _destination network ip_ _subnet mask_ name _name_
- To see only static routes: show ip route static
- Show all configured static routes: show running | include ip route
- L3 switch:
	- ip routing enabled
	- no subinterfaces allowed
	- is not associated with a vlan
	- has ip address
	- does not participate in STP
- show int g0/1 - show single port with physical stats
- show ip int br - show all port statuses and ips
- show ip int g0/1 - show single port with ip related info
- CDP (cisco discovery protocol) - used to mapped a network
	- on by default on supported devices
	- info about hostname, connected port id, ip address, type of device
	- show cdp neighbor
	- show cdp neighbor detail
- LLDP (link layer discovery protocol) - same as CDP, but open source
	- must be enabled, not as detailed as CDP
	- show LLDP neighbors
	- show LLDP neighbors detail
- ICMP (internet control message protocol)
	- sends error and operational info
	- ping and tracert
	- ping 10.1.2.3 loopback 0
	- ping 10.1.1.1 source 10.2.2.2
- route summarization - supernet multiple subnets
	- can black hole unintended traffic
- 

















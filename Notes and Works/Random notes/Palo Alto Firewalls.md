- Panorama - a device that you buy to centrally manage multiple firewalls. Recommended for 6+ firewalls.

# Management Profile
- Network -> Network Profiles -> Interface Mgmt
- To apply on interface: Network -> Interfaces -> select an interface -> Advanced -> Management profile
- Applied to interfaces. Used to permit network services on that interfaces, such as HTTPS, SSH, Ping. 
- A firewall should never be able to be managed from an untrusted port, this increases attack surface. The standard way of remote management is to use a VPN into the private subnet.

# Admin Roles
- Define a role that is applied to an administrator (some user account). Choose specifically which part of the GUI the role can access.
- Device -> Admin Roles

# Address Objects and Groups
- Address Objects - a named representation of IP addresses. can be either a subnet, a domain name, or a specific range of IP. Makes things more readable and easier to manage.
- Address Groups - a group of address objects. Example use case: 3 different web servers that use the same policies, so group their address objects together.
- For Address Objects: Objects -> Addresses
- For Address Groups: Objects -> Address Groups

# Service Objects and Groups
- Same thing as address objects, except for TCP and UDP ports. Example: "Allow HTTPS and SSH" is tried to permitting TCP/443 and TCP/22
- Destination port: akin to destination IP of a server.
- Source port: generally left empty. The source port from the client sending the communication.
- Can apply these to address groups, which makes thing very efficient and clear.
- Objects -> Services || Service Groups
- To apply: ????

# Application Objects
- Like Address Objects, but for applications, such as google, facebook, youtube, microsoft office 365, etc.
- Utilizes App-ID: the firewall updates App-ID signatures from palo alto. This is then used to classify traffic.
- One big problem is that a site like Netflix will rely on many other applications such as Google, so we need to enable all of it for Netflix to work properly
	- https://applipedia.paloaltonetworks.com/
	- Use applipedia to find dependencies for each App-ID.
- Objects -> Applications || Application Groups

# User Objects (Local Users)
- Local users are not integrated with LDAP/AD
- Create local users with a username and password.
- Device -> Local User Database -> Users

# Sync with AD
- https://youtu.be/PIlLdEVZmNE?si=tZ0xME5txTJwTyA2&t=5945

# Zones
- Network -> Zones
- Example Zones: outside, DMZ, inside.
- To add an interface to zone: click on zone -> add under interfaces.

# Interfaces
- Network -> Interfaces
- For subinterfaces, make the main port Layer2, but do not attach it to a zone or attach a vlan. Then select the main interface, and click add subinterface.
- Each interface should have 1 zone. Subinterfaces on the same port can have different zones.
- Layer 3: must be assigned to a virtual router,  assigned IP address
	- The IP address can be an Address Object. This way, it is descriptive, and we can manage the address object instead
	- To make it pingable, make sure to assign a management profile that allows pings
- HA Interfaces:
	- some firewalls come with the 2 HA links, but if they do not, then you must reassign 2 interfaces to become the 2 HA links
	- Assign to HA setup: Device -> High Availability -> gear icon on control link and data link

# V-Wire
- Click on interface -> select type to virtual wire
- To actually configure virtual wire: Network -> Virtual Wires -> Add
- 2 interfaces are configured for a v-wire. They act as if cutting the wire. 
- The firewall is transparent, it only forwards the traffic and applies its security policies. It does not send out its own MAC address and etc.
- Typically used for existing networks, so that you do not have to change or configure existing network configurations
- Need to assign zones to both interfaces. There should be 2 zones, one for ingressing and one for egressing
- Supports VLANs, so the interface can connect to a trunk.
- When setting up the v-wire, check mark Link State Pass through. Basically, if one side goes down, the firewall will force the other side to go down. Avoids unexpected behavior and blackholes.
- If there are subinterfaces on v-wires, you need to connect the parent interfaces and the subinterfaces.

# Security Policies
- Policies -> Security
- A set of rules with corresponding actions. First rule to be matched triggers the action. Implicit deny at the end. 
- Rules can be: source zone, source IP, destination zone, destination IP, App-ID, TCP and UDP ports, URL category (games, malware, gambling, etc).
- Actions: allow. deny (drop traffic, but sends no response to the client). Drop (block traffic and sends TCP reset to the client).
- There are 2 default security policies: allow same zone to same zone traffic, deny different zone traffic. Meaning you must explicitly allow traffic for users to have internet.
- Within service and URL category, you can select the "application-default". This means that the traffic is allowed if the service is using the expected/default port. 
- Source address can be a region instead, so you can block all traffic from Africa for example.

# Virtual Router
- Network -> Virtual Routers
- Assign some interfaces to virtual router. Each virtual router maintains its own routing table. They do not share routing info with each other.
- Traffic between virtual routers must be explicitly allowed via static routes, PBF
- Used primarily for network segmentation: guest and internal, different customers, different departments. 
- Can make it easier to troubleshoot. Can hide info such as OSPF advertisements

# NAT
- 




# Layer 3
- Security policy - a set of rules with corresponding actions. Traffic is matched with first rule, then action is taken on that traffic. If no matches, implicit deny. The action can be block, allow, log this traffic, use threat prevention
- Zones - group of interfaces that share a common security policy, can be virtual interfaces. Example zones: DMZ, Untrust, Trust, Wireless. interfaces must belong to a zone
- Virtual router - a PA firewall can have several logical routers that are independent of each other. Example use case would be different virtual router for each department, if you are CSP, virtual router for each customer. There is always at least the virtual router called "default"


# NAT
1. Login to the GUI.
2. go to NAT configuration window.
3. Select an inside and outside zone. For example, from the "inside" zone to the "outside" zone. 
4. Select the source network, or create a new source network.
5. Select the NAT mode, usually dynamic IP and Port. Select the IP type oof the interface address.
6. Commit to running config.
7. Test: using CLI, test ping from inside zone to outside zone to see if there are matching policies. Test with GUI, built in NAT testing window, enter in the information such as zones to see matching policies.


# Link and Path Monitoring
1. From HA availability, go to Link and Path Monitoring.
2. For link monitoring, create link groups. For each group, add in the links. Groups should be external links and internal links. If ANY of external group goes down, trigger failover. If ALL of internal link goes down, trigger failover.
3. For Path Monitoring, use virtual router path, select default router. Create destination IP groups: many IPs to ping, select if any or all fails, trigger failover. 
4. Commit.
5. Configure the mirror configs on the other firewall.

# Policy Based Forwarding
- PBF rules are evaluated before the routing table. 
- In a HA pair active/passive setup, can be used to steer guest wifi traffic out to backup ISP while still sending main traffic out of main ISP.
1. Select Policy Based Forwarding tab.
2. Select source zone. Can add a source network address
3. Destination/Application/Service: optional, used to match the traffic. For example, match traffic that is going to 9.9.9.9.
4. Forwarding: select forward, discard, or no PBF. Select egress interface, select next hop IP.
5. Commit. 
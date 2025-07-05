- Panorama - a device that you buy to centrally manage multiple firewalls. Recommended for 6+ firewalls.


# Management Profile
- Applied to interfaces. Used to permit network services on that interfaces, such as HTTPS, SSH, Ping. 
- Network -> Network Profiles -> Interface Mgmt
- A firewall should never be able to be managed from an untrusted port, this increases attack surface. The standard way of remote management is to use a VPN into the private subnet.

# Admin Roles
- Define a role that is applied to an administrator (some user account). Choose specifically which part of the GUI the role can access.
- Device -> Admin Roles

# Address Objects and Groups
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


# Security Policies
- A set of rules with corresponding actions. First rule to be matched triggers the action. Implicit deny at the end. 
- Rules can be: source zone, source IP, destination zone, destination IP, App-ID, TCP and UDP ports, URL category (games, malware, gambling, etc).
- Actions: allow. deny (drop traffic, but sends no response to the client). Drop (block traffic and sends TCP reset to the client).
- There are 2 default security policies: allow same zone to same zone traffic, deny different zone traffic. Meaning you must explicitly allow traffic for users to have internet.
- a
1. 

# Policy Based Forwarding
- PBF rules are evaluated before the routing table. 
- In a HA pair active/passive setup, can be used to steer guest wifi traffic out to backup ISP while still sending main traffic out of main ISP.
1. Select Policy Based Forwarding tab.
2. Select source zone. Can add a source network address
3. Destination/Application/Service: optional, used to match the traffic. For example, match traffic that is going to 9.9.9.9.
4. Forwarding: select forward, discard, or no PBF. Select egress interface, select next hop IP.
5. Commit. 
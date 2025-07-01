
1. Hello everyone, my name is Don and I am a senior network engineer at aston technologies. I was tasked with designing the network for the new headquaters of sea ice creamery. This week, I will present my LLD of the wired network and the HLD of the wireless network.
2. As you can see, there are a lot of details, so I think it would be most appropriate to walk through this network from the perspective of a user.
3. A user connects their workstation to an ethernet port. The workstation broadcasts out a DHCP discover message. It travels to the access switch which tags the VLAN, then broadcast it. The SVI on the distribution switch will route the discover message to the DHCP server. The DHCP server will route it back. Through a series of broadcasts, the discover message reaches back to the end user. Through that same procedure of communication, the DORA process is completed, giving the end user the its IP address, default gateway, DNS server, and other information necessary.
4. Lets say the user wants to use the internet, lets say google. The computer would first attempt to resolve google, if it cannot, then it will contact the DNS server to do so. Once it has google's IP, it will see that it is not on the same subnet, so it will forward the packet to its default gateway. The distribution switch will use its default route to the firewalls. The firewalls will route it to the ISP. The ISP will handle the rest. 
5. For the finance department, the only difference is that the distribution switch will also broadcast the discover message, where it will reach the FSP, then the FSP will handle the communication between the DHCP server and the end host. 
6. Notice how there are no SVIs on the distribution switches for the vlans of the finance department. This means that the finance department must use the FSP to be able to communicate to the outside. 
7. The same principle is used for handling voice traffic.
8. There are many redundancy considerations in this design: the network services are configured in HA pairs, there are 2 distribution layer switches configured with HSRP, there are 2 edge firewalls configured in a HA pair, port channels are used to add extra redundancy.
9. The edge firewalls will use bgp to connect to the ISPs. For automatic failover, link and path monitoring should be configured.

# Why Voice Gateway
- Key purpose: There is the public switched telephone network and the regular internet network. They use completely different protocols/technologies to communicate. Voice Gateways bridges the two networks, allowing voice traffic to flow seamlessly across the two networks.

# Why No VDC
- VDC logically separates a single nexus switch into multiple logical switches. The switches are now independent of each other. This could have been used to separate the finance department.
- Adds a layer of complexity to the design. May need to train the onsite IT staff to manage the new technology. But using VLANs will achieve the same result.
- However, if another couple of departments were to be added, then the case could be made to use VDC for efficient management and separating the network.
# Why No vPC
- vPC allows a single end device to connect to multiple nexus switches and treat it as a single logical layer 2 connection. This provides redundancy along with load balancing. 
- This is not necessary because we have another set of network services ready to take over. If more throughput is required, which I do not see it being the case, then a regular port channel can be configured. 

# Virtual Routers in Edge Firewalls
- None because we would use VDCs in the distribution switches.

# Firewall Deflection
- Specific questions regarding the edge firewalls should be directed to the firewall team since I am not aware of the specific security posture of Sea Ice Creamery.

# Wireless Deflection
- Specific implementations and configurations of the wireless topology will be explored in the next part of the project.

# General Deflection
- That is a great question, I can get back to you on that after this presentation.
- That is outside the scope of this presentation, but I would be more than happy to discuss that with you after the presentation.
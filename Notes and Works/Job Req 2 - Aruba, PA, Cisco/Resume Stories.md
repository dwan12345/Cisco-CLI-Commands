
- Managed firmware and software upgrades on Catalyst 9500 switches, ensuring compliance with security policies and leveraging new features and enhancements for continuous network improvement
	1. figure out the scope of the change: which switches need to be upgraded?
	2. do some research about the version we are upgrading to. is it compatible with our specific switch model? 
	3. create step by step instructions, verification plan, and backout plan
	4. have it peer reviewed
	5. present it to the CAB. This gives other departments the chance to bring up their specific interests in the change. it also creates awareness for the change because there might be downtime
	6. schedule downtime, usually out of usual business hours
	7. now we can perform the update. we used a scp server
	8. backup the existing configs: copy run scp:// \<ip>/config/\<name of switch>/
	9. transfer the new img: copy scp:// \<ip>/img/\<name of switch>/\<img name>.bin flash:
	10. change where the switch boots from: boot system \<img name>.bin
	11. write mem
	12. reload the switch
	13. verify that the change worked. the most basic stuff would be to ping the internet and to make sure core resources are available
	14. wait and monitor the situation
	15. if something breaks, perform the backout plan
	16. make sure to document along the way. was the change successful, what went poorly, what went well, any special considerations that we had to take that other people should be aware of
- Engineered, deployed, and maintained Cisco Viptela SD-WAN fabric across enterprise branch locations, utilizing vManage to configure vEdges, establish secure IPSec tunnels, and automate device onboarding
	1. gather the necessary information such as network topology, IP scheme, and security requirements.
	2. deploy the vManage. perform the initial setup, IP, DNS, NTP, certificates, AAA server
	3. onboard the vSmart and vBond. add the serial and chassis numbers to vManage. create certificates, sign it, attach it to the appropriate devices. make sure you can see the vSmart and vBond in the vManage
	4. configure ZTP services
	5. add the vedge using the serial and chassis numbers
	6. ship the vedge to the remote location
	7. connect the vedge to the internet, and it will automatically attach itself to our SD-WAN fabric
	8. create feature and device templates
	9. apply the tempate to the vedge
- how do you set up ZTP for Viptella?
	1. Add the vedge to our cisco smart account. usually added when we buy
	2. our vbond must be reachable via the internet
	3. assign a device template to our vedge in vmanage
	4. set up the DNS resolution of our vBond, which is done in the cisco smart account
	5. when the vEdge is plugged in, it will contact cisco's servers to find our vBond
	6. the vEdge automatically forms the tunnel and downloads the configs
- how to set up Aruba Controllers in HA?
	1. ensure that both controllers are the same model, software version, license, and NTP. there are two scenarios in doing this: when you have a mobility conductor, and when you have a standalone mobility controller.
	2. for both setups, you need to connect the two devices with a direct link.  for failure detection, sync the devices. 
	3. for standalone HA, create an HA group. add both controllers to the HA group while providing the IPs of each controller.
	4. enable config syncs, and heartbeats. enable preemption if you want to. then deploy
	5. verify by look at the HA GUI page.
	6. for mobility conductor setups, go to the GUI of the mobility conductor
	7. create a cluster, which will represent our HA group. add the necessary controllers to the cluster while providing their IPs. 
	8. configure VRRP for the cluster. make sure to add VIP. configure priority and premption if you want. add the password
	9. verify setup by looking at the controller cluster GUI page, they should be up.
- how are licenses handled by Mobility Conductors?
	- we buy licenses which will be placed into a pool
	- whenever we activate a device, such as an AP or a Mobility Device, it takes the appropriate license from the pool. If the MD is using features that require additional licenses, it will take those from the pool
	- if a device no longer needs the license, the license will be added back to the pool
	- if a device loses connection to the MC, it will continue to operate, but we will have limited ability to configure the devices. Such as we cannot activate new licenses and new APs cannot be added 
- Troubleshot advanced SD-WAN issues, including overlay connectivity failures, BFD session drops, and QoS problems, using vAnalytics, logging, Wireshark packet captures, and CLI commands
	- follow the general troubleshooting best practices: define the problem, isolate it, gather information, formulate a hypothesis, test it, form a plan, do CAB meeting if necessary, apply plan, document
	- make use of the dashboard to get an overview of the situation. check any error messages, they are always a great place to start.
	- check the logs for any useful messages. show commands
	- last but not least, packet captures with analysis using wireshark
	- overlay connectivity: check the show commands and logs to see if the tunnels are being created properly. commonly caused by certificate issues, or firewalls.
	- bfd session drops: check the show commands for bfd to see the health of the link. check the latency, jitter, and packet loss for the underlay. check logs. commonly caused by underlay issue such as high cpu usage on vedge, interface errors, network congestion. 
- What were your day to day activities at CRA International?
	- deployed and managed cisco catalyst and nexus switches. configured the routing protocols, and managed software upgrades. configured vPCs on the nexus switches. deployed and managed vEdges. managed palo alto firewalls such as security zones, security policies, global protect VPNs. and of course, troubleshooting any issues.
- Set up complex NAT rules and IPsec VPN tunnels on Palo Alto firewalls, ensuring secure communication between remote sites and managing overlapping IP addresses
	- set up the IPsec tunnel
	- determine the network resources that need to be accessed on both sites
	- designate an IP scheme that does not conflict with either site. We will use this for all of the NAT rules.
	- create DNAT rules for the resources that need to be accessed. 
	- create SNAT rules on each firewall so that hosts try to access resources at the other site, their traffic's source IPs get translated to the IP of the tunnel on the firewall.
	- if you need to create DNS records, make sure to account for the fact that for each site, DNS should respond back with a different IP.
- talk about network security compliance
	- in general, for a lot of security compliance, the minimum is implementing network segmentation, have NAC, have encryption, logging, and secure configurations. network segmentation can be implemented using VLANs, VRFs, virtual systems. NAC is implemented using AD server with some kind of NAC solution, such as cisco ISE, then syncing that with your networking devices. Encryption typically involves using VPNs and IPsec tunnels to communicate to the outside. Logging involves setting up a syslog server and pointing our network devices there. Secure configurations involve following best practices from vendors as well as changing the default logins. 
- 
- operation turnover documents, how does excel work in network, 
- what are ways to remotely access the vEdge if the overlay goes down?
- 







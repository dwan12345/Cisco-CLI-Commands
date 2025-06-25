- What devices are the voice gateways and are there any special considerations for them in the network?
	- Cisco ISR 4431
- What are the IP addresses to your ISPs along with their AS numbers? What is your AS number? Are there any other details you would like to bring to my attention regarding the connection to the ISPs?
Local AS: 6211 
Local Int: 68.136.143.66/30 
neighbor 68.136.143.65 remote-as 65000 
neighbor 68.136.143.65 password 7 0961612A542702010202013938 
**Century** 
Local AS: 6214 
Local Int: 152.162.97.182/30 
neighbor 152.162.97.181 remote-as 65510 
neighbor 152.162.97.181 password 7 09617E2A5423051D05180D2F39 
Note: Each ISP has been asked to only share a default route

- Can you provide a WIFI strength map.
- Other than the default route from the ISP, are there any other filters that you would like me to take into consideration? What about BGP route attributes?
- For Comcast, is the Handoff a fiber port or ethernet port? What about for Century Link?
- How does the voice data from the financial department move through the network? Is it supposed to reach the voice gateway? Or does it get processed by the FSP?
- what is the domain name of your 





- The low level wired diagram does not need the APs and WLCs right? Do I have to include the APs and WLCs in GNS3? The LLD does need the APs and WLCs, but not in GNS3
- In GNS3, can I use routers for the firewalls (both FSP and edge), routers for the DHCP server, VPCs for the phones, and routers to simulate the ISP connection? Don't worry about GNs3 all that much. Focus on the wireless HLD and the physical LLD
- what do I do for DNS?
- Within ezWifiPlanner, it does not have cisco APs, should I one that is similar to my cisco AP in strength?
- I have my wireless vlan and my mangement vlan, from which vlan should my APs get their ip addresses?
- 
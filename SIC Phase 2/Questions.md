## Email Questions
1. What requirements are there to connect the financial services proxy (FSP) server to the network? Isthere a pair of FSPs?
We will be using a Palo Alto NGFW 820 as the FSP. We have the following connection requirements: 
    The Finance Security Proxy will be configured to ensure that the FD only has access to approved resources. The proxy is going to have 2 interfaces: an “inside” interface which traffic coming from the finance department MUST enter. An “outside” interface where we will forward traffic which has been approved by the proxy to go to the rest of the network. 
    We’ve been thinking of creating subinterfaces on the inside interface to facilitate both the Data and Voice networks in the Finance Department, and then applying the default gateways of those networks to the interfaces as a VIP providing failover. That will force all the traffic through the proxy. Then all we need is a couple outside interfaces which are L3 adjacent to the primary campus network and a next-hop IP for the static route. 
    If that all sounds good to you, we’ll need: 
    ·       2 Finance Data IPs (and what VLANs they are on) 
    ·       2 Finance Voice IPs (and what VLANs they are on) 
    ·       Finance Data Default Gateway IP 
    ·       Finance Voice Default Gateway IP 
    ·       2 IPs which have access to the primary network for my outside interfaces 
    ·       1 VIP IP in the same subnet as my outside interface IPs to act as the “next-hop” IP for traffic returning to the Finance Department. 
    Last, but not least, we’ll need to know the next-hop IP for the proxy’s default route to forward traffic to the primary network. Let us know if you have any questions! We welcome suggestions as well..
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

1. For the purposes of placing the APs, can you provide me information regarding the types of walls on the floor? The exterior walls will be preformed concrete slabs, the interior walls will be timber framed drywall.
2. Other than the default route from the ISP, are there any other filters that you would like me to take into consideration? What about BGP route attributes? None at this time.
3. For Comcast, is the Handoff a fiber port or ethernet port? What about for Century Link? That information is on the floorplan document.
4. How does the voice data from the financial department move through the network? Is it supposed to reach the voice gateway? Or does it get processed by the FSP?  It is routed from its default gateway on the FSP to the appropriate voice gateway.
5. What is the domain name of your company. @seaicecreamery.com

6. Does your company have an established naming scheme for your network devices? nope
7. Do you guys plan to use the edge firewalls in an active/active or active/passive setup.



## Non role play questions

- The low level wired diagram does not need the APs and WLCs right? Do I have to include the APs and WLCs in GNS3? The LLD does need the APs and WLCs, but not in GNS3
- In GNS3, can I use routers for the firewalls (both FSP and edge), routers for the DHCP server, VPCs for the phones, and routers to simulate the ISP connection? routers for DHCP, firewalls, voice gateway.
- Should the LLD include details about the type of cable between 2 devices? u can if u want
- I have my wireless vlan and my mangement vlan, from which vlan should my APs get their ip addresses from? wireless vlan
- So I created a floor plan in ezWifiPlanner, added the obstables, used a similar strengthed ECW AP to my cisco AP to have it automatically place the APs. Is there anything else that should be on the wireless HLD?
- 
- what do I do for DNS? not actually any function
- 
- 
- 
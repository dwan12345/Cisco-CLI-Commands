
# Initial Setup
1. plug the RAP into power and turn on.
2. plug the RAP into the router/modem at the remote site.
3. the router will have DHCP, which gives the RAP its IP address, domain name (the company's domain), and the DNS server (the router)
4. RAP will attempt to discover the IP address of our Mobility Controller (WLC)
	- there are 2 ways to do this: DNS, and Cloud Activation. the DNS way is described below
5. it attempts to resolve aruba-master.\<domain name>.com
6. Our router will forward to the local DNS server, then it goes to root, then to TLD, then to the authoritative DNS server controlled by our company. 
7. Our company's DNS server will reply with the public IP of the mobility controller. 
8. RAP forms an IPSec tunnel over the internet to our mobility controller. the RAP verifies itself using certificates or PSK.
9. the RAP downloads the configurations, which includes:
	- SSID
	- security policies (WPA3, client authentication methods)
	- VLAN assignments for ports and virtual ports
	- routing polices and firewall rules

# Client Connection
1. a client sees the SSID and connects to it
2. the client has to authenticate. the authentication request is forwarded back to the mobility controller. the mobility controller gives the client its IP address, roles, etc.
3. client can now connect to the internet

# Client Traffic Flow
1. client access the internet
2. the traffic goes to our RAP, which encrypts it and sends it to our mobility controller
3. the mobility controller forwards it through our main network, which has firewalls, proxies, etc. So out security policies are enforced, remote users can access company resources, and everything is centralized
4. the traffic reaches our corporate network edge and is then forwarded to the internet
5. the return path of the traffic is self-explanatory




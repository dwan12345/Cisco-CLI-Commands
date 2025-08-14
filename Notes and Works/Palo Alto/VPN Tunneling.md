- can configure site to site tunnels and GlobalProtect
- GlobalProtect - allows remote clients to securely connect to our network. the GlobalProtect client must be installed on the client
	- can configure context aware access control, say deny access if the user has really old OS
	- Portal - where the client goes to authenticate
	- Gateways - client chooses which gateway to use to establish the tunnel. This is where the tunnel is created and the data is moved around




# Site to Site Tunnel
- information required
	- Phase 1: peer IPs (the public IPs), encryption type, hashing type, DH group number, PSK, key lifetime 
	- Phase 2: protocol, encryption type, hashing type, PFS or no PFS, key lifetime
- configure IKE crypto profile. like an ISAKMP policy in cisco
	- network -> network profiles -> IKE crypto -> add
	- add all of the information
- configure IPsec cypto profile. like creating the IPsec in cisco, remember it was the second thing that you configure.
	- network -> network profiles -> IPsec crypto -> add
	- add all of the info
- configure IKE gateway. the object that is actually doing the VPN
	- network -> network profiles -> IKE Gateways -> add
	- interface: select the outside interface
	- Local IP address: the outside interface IP
	- Peer Address: self explanatory
	- add the PSK
	- in advanced options, select the IKE crypto profile
	- if the PA is behind a router running NAT, go to advanced options, enable NAT-T. there may be more stuff you need to configure for this to work
- create the IPsec tunnel
	- tunnel interface: create a new tunnel interface. the tunnel interface should have a new zone attached to it to have fine grain control
	- IKE gateway: select the gateway we just created
	- IPsec crypto profile: select the profile we created in the beginning
	- Proxy ID: specifies the local and remote subnets that are allowed to talk to each other. on both ends must be an inverse of each other. do more research
	- commit
- create a route that will use the tunnel
	- network -> virtual routers -> *select the router* -> static routes -> add
	- destination: destination subnet
	- interface: select the tunnel
	- next hop: none
- create a new security policy allowing our zone to the tunnel's zone
- create a new security policy allowing our tunnel's zone to our zone
- verify
	- go to CLI of the PA: test vpn ike-sa gateway \<the gateway we made> 
	- go to CLI of the PA: test vpn ipsec-sa tunnel \<name of the tunnel>
	- network -> ipsec tunnels 
		- you should see green bubbles for it being up
		- if you do not have traffic that goes through the tunnel or you do not test the tunnel, then the tunnel may show as down even if it is configured correctly
	- ping from a local device to the other end
	- network -> ipsec tunnels -> *click on the tunnel*
		- the pkt encap should be increasing as you ping more








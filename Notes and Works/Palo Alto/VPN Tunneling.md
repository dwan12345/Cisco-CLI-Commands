- can configure site to site tunnels and GlobalProtect
- GlobalProtect - allows remote clients to securely connect to our network. the GlobalProtect client must be installed on the client
	- can configure context aware access control, say deny access if the user has really old OS
	- Portal - where the client goes to authenticate
	- Gateways - client chooses which gateway to use to establish the tunnel. This is where the tunnel is created and the data is moved around




# Site to Site Tunnel
- information required
	- Phase 1: peer IPs (the public IPs), encryption type, hashing type, DH group number, PSK, key lifetime 
	- Phase 2: protocol, encryption type, hashing type, PFS or no PFS, key lifetime










# Filtering
- Prefix list - match exact prefix. 
	- filter BGP: neighbor [neighbor IP] prefix-list PREFIXLIST in
- route map - match a prefix list, and can match other route attributes
- Direction:
	- relative to local router: inbound and outbound
	- filtered routes are not added to bgp table
	- in outbound, bgp table gets filtered
- Soft reconfig inbound - cache/buffer to store the complete advertisement from peer. Used for troubleshooting and for soft resets
- ACL:
	- generic list of permit and deny statements
	- used for basic security
	- identify interesting traffic and filter it
	- standard: based only on source IP
	- extended: matches based on source and dest IP, protocols, and ports



# Alternative NAT and IPsec
- IPsec tunnels: create a logical point to point connection between 2 remote sites. encrypted.
	- Connect 2 physcially distant LAN, sometimes business to business tunner (B2B)
	- client VPN allows users to remote access to a network
	- Phase 1: management tunnel, IKE_SA_INIT, used to build the second tunnel
		- exact match of security associations: hashing, authentication group, encryption, Diffie hellman group
		- tunnel init -> SA exchange -> established -> management traffic flows
	- Phase 2: encapsulated inside phase 1 tunnel, data flows through this
		- A separate set of SAs, must match on both sides: protocol (AH or ESP), encapsulation method, encryption, authentication, perfect forward secrecy (optional)
		- management traffic -> tunnel init -> exchnage SAs -> tunnel up -> traffic flows
	- Version 1: uses more bandwidth
	- Version 2: supports more EAP authentication, NAT traversal built in, built in keep alive mechanism to keep tunnel up. 
	- 3 methods of encryption: DES (least secure), 3DES (medium security), AES (most secure)
	- Authentication methods: verifying that you are who you are. Using PSK or certificate
		- AH: authentication header, unsecured
		- ESP: encapsulation security payload, can be secured
	- Transport mode: uses original IP header
	- tunnel mode: encapsulates original packet, then gives ne IP header. commonly used for site to site
	- Hashing: verify integrity of packets
		- MD5
		- SHA: uses Diffie Hellman group
	- VTI: virtual tunnel interface. logical layer 3. used as endpoints for tunnels. Can be dynamic or static defined, dynamic is used for hub and spoke topologies like DMVPN.













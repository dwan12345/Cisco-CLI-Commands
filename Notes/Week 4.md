

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

















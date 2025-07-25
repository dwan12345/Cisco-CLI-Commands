
# Layer 2 Forwarding
- uses ASICs (Application specific integrated circuit) and CAM (content addressable memory) to essentially perform hardware lookups of exact match MAC addresses to be super quick
- ASIC: chips made for a specific purpose
- CAM: specific memory used by switches for rapid MAC address lookups

# Layer 3 Forwarding
- much more complicated than layer 2 because instead of exact matches, partial matches are good
- the router also needs to reduce the TTL, recompute the IP checksum, recompute the ethernet FCS
- Uses ASICs with TCAM (Ternary Content Addressable memory) to perform some hardware level forwarding
- TCAM - instead of exact matching (1s and 0s), offers 1s, 0s, and Xs, where Xs can be anything, which allows for things such as longest prefix matching

# Software Based Router
- make forwarding decisions in software using a general purpose CPU
- very slow, but flexible as you can repurpose regular computers as networking a networking device

# Hardware Based Router
- purpose built machines for routing
- general purpose CPU handles the control plane, such as OSPF, static routes
- purpose built ASICs are used for data plane

# Hybrid Router
- general purpose CPU does control plane
- the Network Processor (NP) is used for forwarding data
- NP - specialized processor for forwarding packets. A balance of perform and flexibility, since they are

# Process Switching
- not switching ethernet frames, this is switching IP packets
- uses the CPU, so it is only used when necessary, such a complicated packet arrives that CEF cannot handle
- Steps:
	1. receive packet
	2. check routing and arp table to see which interface to forward out of.
	3. forward out of the interface
- Fast switch - the same thing as process switching, but now there is a cache
	- it is generally no longer supported today because there is no reason to use this over CEF

# CEF
- the default packet switching mechanism
- CEF is implemented on all types of routers. Software CEF is much faster than process switching but not as fast as hardware CEF
- TLDR: for layer 3 switching, precomputes forwarding info and stores it in a specialized data structure, which allows for fast hardware based lookups and forwarding
- CEF is comprised of the FIB and Adjacency Table
- Forwarding Information Base (FIB) - built from the RIB (the routing table), quickly find the next hop IP. This info is stored in memory in the TCAM
- Adjacency Table - built from the ARP table, essentially prebuilds the ethernet header to forward. Quickly finds the outgoing interface.

# Distributed CEF (dCEF)
- only on chassis routers
- a copy of the CEF databases are stored on each line card, which is then used to do the forwarding decisions


# Commands
- see the FIB
	- for next hop: "no route" only appears for default route, when it is not configured. "drop" means to drop the packet, ie 127.0.0.0/8 or reserved IPs, "receive" is packet for the router itself such as loopbacks and interface IPs, "attached" basically connected routes in the routing table
```js
show ip cef
```
- see the adjacency table
```js
show adjacency
```



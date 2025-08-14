- Multi Protocol Label Switching - like how routers uses IP switching and switches uses MAC switching, they used labels to switch
- MPLS header is inserted between the ethernet header and IP header
- MPLS header is 32 bits
- The original reason for this was because IP switching was too slow, adding a label and switching off of that made it much faster in the old days
	- with faster hardware and better switching techniques, this benefit is negligible nowadays
	- Modern use cases:
		- for layer 3 VPNs
		- allows the ISP to run a single routing protocol (MPLS) despite their customers having different protocols
		- customers will use private IP. There are networks that allow customers to route private IPs across the ISP to another location of the customer's (Route Distinguisher)

# Routers
- Customer Edge (CE) Router - the router the customer connects to
- Provider Edge (PE) Router - the router that connects to the customer's domain
	- analyzes the IP header, calculates the appropriate MPLS header to add. 
	- Forwards to internal ISP network, which will only route based off of the label. The internal network will rewrite the label as necessary and forward it.
	- the MPLS labeled packet will reach the PE that is closest to the destination, which will just route the packet normally to the destination CE.
- Label Switch Routers (LSR) - the internal ISP routers that only route based on labels.
	- Uses Label Distribution Protocol (LDP) to distribute the labels, like a dynamic routing protocol

# Configuration Notes
- 
# Configure MPLS
- must have a dynamic routing protocol running
- every interface connected to another LSR should have mpls ip
```js
! configure mpls on an interface
conf t
ip cef
mpls ip
int <interface> 
	mpls ip
	end
```
- instead of manually configuring mpls on each port, use autoconfig instead
	- every port participating in ospf will send out LDP hellos
	- no equivalent for eigrp
```js
! configure mpls autoconfig
conf t
ip cef
mpls ip
router ospf <process id>
	mpls ldp autoconfig
	end
```


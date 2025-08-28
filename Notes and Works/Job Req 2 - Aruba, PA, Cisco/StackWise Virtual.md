
# General Notes
- used for 9300, 9400, and 9500 switches
- creates a single logical switch from 2 switches
- can only stack 2 switches
- a switch can only be a part of 1 SVL domain


# Link Types
- StackWise Virtual Link (SVL) - carries control and data traffic between two stacked switches
	- should be port channel of at least 2 ports that are at least 10 gig
	- the port channel links should using different line cards
	- should be directly connected. not routed link
- Dual-Active Detection (DAD) - for preventing split brain. 
	- can be directly connected, not routed link
	- can be BFD routed link when distance is far.


# Failure Scenarios
- when SVL goes down but DAD is up
	- standby switch shuts down all of its data interfaces. it stops forwarding data traffic
- DAD is down but SVL is up
	- no impact, just logs
- both SVL and DAD are down
	- self explanatory. split brain. severe network instability. 





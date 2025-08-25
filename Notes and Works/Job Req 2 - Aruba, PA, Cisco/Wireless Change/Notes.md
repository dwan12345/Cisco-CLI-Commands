# Terms
- passive site survey - listening to the existing wireless environment, but never connecting to the WIFI
	- done with a laptop with a specialized software
	- collects signal strength, noise levels, interference sources, AP coverage, signal to strength ratio, channel overlap and utilization.
	- used for pre deployment to see where to place APs
- active site survey - connects to the WIFI and transmits packets to simulate real user.
	- measures throughput, latency, packet loss, signal strength, retransmission rate, roaming behavior
	- used for post deployment verification to see if the environment meets performance expectations
- predictive site survey - uses floor plans to build a virtual environment to simulate the actual wireless environment
	- used for initial planning and budgeting to estimate roughly how many APs
	- used for large deployments which can save a ton of time

# Documents Needed
- topologies, both physical and logical
	- for IP scheme, vlans
	- security design: AAA server, guest access control, WPA3
	- what POE version do the switches support
- floor plans, building plans, material information.
	- so that we can map out our design
- passive and active site surveys

# Customer Questions
- what applications are we supporting?
	- how many applications
	- throughput requirements?
- how many clients?
	- device types that they will be using
	- do client counts vary throughout the day?
	- which part of the buildings might have a large number of clients?

# Pre-Site Survey Checklist
- client contact info
- number of sites, buildings, floors
- size of the buildings and floors
- business/operation hours
- addresses
- user count, application requirements
- RF coverage
- existing infrastructure
- knowledge of average packet size








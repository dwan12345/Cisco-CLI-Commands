- Priority Group - assigned within a pool, assign some nodes to be in a higher priority group. The load balancer will only forward to the highest priority group until a Priority group activation is triggered. higher priority group number is prioritized
	- priority group activation - say there are 3 servers in priority group 1. We say if there is 1 or less healthy server in this priority group, then start using priority group 2
	- provides controlled failover
	- you can have backup cloud resources that are only used when on-prem resources are exhausted 
- Configuration steps:
	1. Local traffic -> pools -> *select pool* -> members -> priority group activation
	2. Select "less than" and pick how many healthy servers before falling back to a lower priority group
	3. Below that, there are member nodes, click into it to change the priority group number.
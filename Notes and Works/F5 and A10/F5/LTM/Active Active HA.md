- still configure the device group, refer to active passive HA, but this time we will use at least 2 traffic groups. Each traffic group should serve a different kind of application. The idea is that each traffic group has a different Active F5 and failover to the other F5.
- for each traffic group, we assign a different order of failover
- for each traffic group, we create new floating IPs for the both internal and external
- since this is designed to serve 2 different applications, 2 VS with their corresponding pools must be created

# Configuration
- Requirements
	- device group of at least 2 F5 are already configured
	- at least 2 virtual servers with different pools serving different applications
- create another traffic group
	1. device management -> traffic groups -> create
	2. name it
	3. under failover configuration, use "failover using preferred device order"
	4. use a preferred order that is different than the first traffic group
- create the new floating IPs
	1. network -> self IP -> create
	2. create an internal IP assigned to the second traffic group
	3. create an external IP assigned to the second traffic group
- assign the VS to a traffic group
	1. local traffic -> virtual server -> *click on your VS* -> properties
	2. under traffic group, select the second traffic group
- make sure to sync
- verification
	1. start using both applications
	2. go to CLI of each load balancer
	3. use "tmsh show sys connection | grep " to determine if the connections are going through different F5s. You can grep for port number or IP address
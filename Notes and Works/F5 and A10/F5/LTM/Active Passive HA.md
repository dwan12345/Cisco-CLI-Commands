# Device Servicing Cluster (DSC)
- feature used by F5 to implement HA
- usually configured in active-standby, but can be active-active
- Device Trust - used to securely communicate and synchronize data between BIG-IP devices
- Device Group - collection of trusted BIG-IP devices that are configured to sync their configurations
	- Sync Failover Group - devices in this group sync their data, and can failover
	- Sync Only Group - only syncs their data. Only for consistent configurations
- Requirements: 2 BIG-IPs with the same software version. Dedicated HA interface/VLAN. proper licensing. NTP sync. Basic network connectivity. Allowed necessary ports for HA, port 4353, 1026
- Interfaces and IPs:
	- each F5 must have management IP 
	- each F5 must have interface connecting to the inside network. 
	- each F5 must have interface connection to the outside network
	- the 2 F5s connect using an HA interface, they are routed with IPs in their own subnet and vlan
	- floating IP address for internal
	- floating IP address for external

# Config
- must mirror this on both/all F5 devices
1. network -> vlan -> vlan list
2. ensure that internal and external vlans are already created with their associated interfaces
3. create a new vlan exclusive for HA. click create.
4. give it a name. Tag is optional. Add the appropriate interface, untagged or tagged, based on the network. click finished
5. network -> self ip -> create
6. Give it a name, the IP and mask of the interface used in HA, select the HA VLAN we just made, port lockdown of Allow Default.
7. click finished
8. device management -> devices -> *click on the self device* -> configsync
9. pick the HA self IP we just created
10. device management -> devices -> *click on the self device* -> failover network
11. Add all of the self IPs on port 1026 except for the HA self IP
12. device management -> devices -> *click on the self device* -> mirroring
13. For primary, select the HA self IP. For secondary, select the internal self IP
14. device management -> device trust -> peer list -> add
15. You can do this step on just 1 F5 because they will exchange their certs and trust each other. Add the management IP of the other device, admin username and PW. Click Retrieve device info
16. device management -> device group -> create
17. Only 1 device. give it a name, group type to Sync-Failover, add all of the members. Finished
18. Only 1 device. Top left, click awaiting initial sync. click sync.
19. A traffic group is automatically created when you created the device group
20. device management -> traffic group -> *select the traffic group*
21. not necessary, but a bunch of configuration options here
22. Now we need to create the floating internal and external self IPs. This only needs to be created on one device since we are attaching it to the traffic group associated with the HA cluster, the device will propagate that info out to the others
23. network -> self ip -> create
24. Internal: name, floating IP of internet network, vlan of internal, traffic group of the HA group we just made (it will say floating). click finished
25. Do the same for external
26. device management -> overview
27. make sure to push the changes 
- Wait a minute for them to sync, then to verify:
	- device management -> overview
	- login to the different F5s, top left should say active or passive, and In Sync
- to force active F5 to standby:
	1. go to GUI of active device
	2. device management -> devices -> *click on self device*
	3. scroll down. click Force to Standby
- 3 HA links are needed
	- some firewalls come with these 3 links, others you will have to use the regular interfaces
	- HA1-A - the control plane traffic. keep alives, config syncs
	- HA1-B - backup for HA1-A
	- HA2-B - the data plane traffic
- same hardware, software version, licenses
- the passive firewall should have no configurations to prevent initial sync failures


# Active-Passive
- there is no VIP, instead both PAs will share the same IP for the inside and outside interface. virtual MAC and gratuitous ARP is used. This means that the inside interfaces of the PAs have to connect to the same switch, and the outside interfaces of the PAs have to connect to the same switch.
- you need to configure this on both firewalls
- Change the interfaces to be in HA mode
	1. network -> interfaces
	2. click on an interface. change the interface type to HA
	3. do step 2 for 3 interfaces
- configure HA cluster
	1. device -> high availability
	2. within setup: enable HA. make sure group ID matches on both firewalls. select active-passive. enable config sync. enter the peer's HA1 IP and the peer's backup HA1 IP
	3. within active-passive settings: set to auto. set fail hold time to 1 min
	4. within election settings: lowest priority number becomes active. enable preemptive
	5. within control link HA1: select the correct port. put in the IP and subnet mask. 
	6. within control link HA1 backup: select the port. put in the IP and subnet mask.
	7. within data link: select the port. 
	8. commit
- to verify
	- dashboard -> widgets -> HA
	- configure something on the active PA, commit, wait for passive PA to sync, check the passive PA to see configuration
	- device -> high availability -> operational commands: suspend local device. make sure clients can still ping

# Link and Path Monitoring
- configure this on both devices
- device -> high availability -> link and path monitoring
- link group
	1. add
	2. any failover condition
	3. add some interfaces. if any of those interfaces go down, then the PA will perform failover
- Path Group
	1. add virtual router path. this uses a ping to test path connectivity
	2. select the virtual router
	3. select all failover condition
	4. add at least 2 public IPs. if all of those IPs are unpingable, then failover
	5. commit
- to verify
	- disable a port to the internet to test

# Active-Active
- there will be a VIP. The inside and outside interfaces of the PAs need to have different IPs.
- start by configuring active-passive
- configure the interfaces with the appropriate IPs on both PAs
	1. network -> interfaces
	2. select the interface that connects to the ISP
	3. change the IP address to another
	4. select the interface that connects to the internal network
	5. change the IP address to another
	6. repeat for second PA
- change to active-active. Do this on both devices
	1. device -> high availability
	2. within setup: change to active active. the device ID has to be different on each PA
- configure HA3 interface on both PAs: for when traffic flows out of PA 1, but flows back into the network through PA 2, HA3 is used to move that traffic from PA 2 to PA 1 to ensure session stability
	1. network -> interfaces
	2. select the interface that will be used for HA3, change type to HA
	3. device -> high availability -> Active/Active Config
	4. within packet forwarding: change HA3 interface to the interface we just configured. check mark VR sync. Session owner selection set to first packet. 
	5. commit
- configure VIP. you only need to do this on one PA
	1. device -> high availability -> active/active config
	2. under virtual addresses, click add
	3. select the interface that is on the inside
	4. click add for IPv4
	5. type in the floating IP
	6. select ARP load sharing
	7. do steps 2-6 for the outside interface
	8. commit
- configure NAT for the external VIP. do this for only 1 PA. this is to make sure that when a PA fails, the current NAT connections do not get interrupted since both PAs will have the NAT translations
	1. policies -> NAT -> add
	2. within original packet: source zone of inside, destination zone of outside, destination interface of the outside interface
	3. within translated packet: translation type of dynamic IP and port, add a translated address and put in the external floating IP
	4. within Active/Active HA binding: select 0.
	5. clone this NAT policy
	6. within the clone, change the Active/Active HA binding to 1
	7. commit
- to verify
	- dashboard -> HA widget: after enough time to sync, everything will be green. this does not verify the VIP
	- continuously ping the VIP, then suspend the local device, then see if it auto failover








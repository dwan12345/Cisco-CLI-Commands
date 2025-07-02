
## WLC
- WLC connects to switch via LAG (Link Aggregation Group). WLC only supports static LAG, no PAgP or LACP. The port channel should be a trunk with all of the VLANs
- Make sure there is a reachable DHCP server
- LAPs connect to switch interface that is set to access and with the management VLAN. Should be portfast as well
- 


## WLC Initial Setup
- connect via console port
- walk through setup wizard
- Make sure the management interface IP and VLAN ID is within the management vlan in the actual network

## Config on WLC
- Connect to WLC GUI via web browser and type in the management interface IP configured on WLC
- Controller: create a new interface for each vlan
	- Configure the physical port (usually the port channel)
	- VLan ID
	- IP address and netmask (the IP and subnet mask of the port channel)
	- gateway (probably SVI of L3 switch or a router)
	- DHCP server IP
-  WLAN: creating new Wi-Fi areas. 
	- Profile name: anything, usually the same as SSID
	- SSID: self explanatory
	- ID: unique for the WLC for each WLAN but it is arbitrary
	- General Tab
		- status: set to enable
		- interface: set to the appropriate interface (guest Wi-Fi set to guest interface)
	- Security tab:
		- Layer 2 security: WPA+WPA2
		- Enable WPA2 policy
		- Select PSK (pre-share key) in authentication
		- type the PSK password
	-  












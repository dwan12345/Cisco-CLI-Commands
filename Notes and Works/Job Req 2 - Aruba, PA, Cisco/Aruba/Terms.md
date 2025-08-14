- Dynamic Frequency Selection (DFS) - 
- Orthogonal Frequency Division Multiplexing (OFDM) - 
- Aruba Central - network management platform for aruba wired, wireless, SD-WAN
- ArubaOS - the OS for aruba WLC and APs
- ArubaOS-CX - the OS for switches
- Aruba Edge Services Platform (ESP) - 
- Virtual Switching Framework (VSF) - a tech that allows aruba switches to stack together
- Dynamic Segmentation - 
- ClearPass - aruba's NAC solution. like cisco ISE
- NetConductor - 
- AIOps - 
- Policy Enforcement Firewall (PEF) - arubas solution. enforces security policies at the network edge

# Actual Terms That I See
- Aruba Remote Access Point (RAP) - provides wireless services to a remote site. once connected to the internet, this device forms a VPN tunnel to the Aruba Mobility Controller, receives its configurations, and works. can also provide wired services
- Aruba Mobility Controller - the WLC for Aruba 
- Controller Hierarchy 
	- Managed Devices - APs establish tunnels with this controller. data is forwarded, authentication requests, etc. Sends heartbeats to the master controller. can be configured to do failover to another local controller or even the master controller
	- Mobility Conductor - the network admin is mostly working with this to push global config changes. centralizes licensing. organizes local controllers into groups to apply configs consistently. it contains config templates for the APs which are distributed to the local controller. it centralizes management
- Airwave - Aruba's on-premises solution for managing and monitoring wireless and wired network infrastructure
- ClearPass - aruba's NAC solution. like cisco ISE
- BSS - the wireless service provided an AP that clients can join
- BSSID - the unique identified for the AP. will be based on the MAC address
- ESS - combo of at least 2 BSS. provides roaming. when the client's signal gets too weak to the AP, it disassociates, then it scans for another AP with the same SSID, once it finds one, it reassociates.
- AirMatch - automatically selects the channels for the APs, optimizes the channel power, 

# Frames
- management frames
	- beacon frames: sent by APs to advertise the SSID
	- probe frames - how your wireless device discovers SSIDs. probe response is sent by AP, which contains the info necessary for the client to connect
	- authentication and deauthentication frames - 
	- association and deassociation - 
- Control frames
	- ack - acknowledge unicast
	- block ack - acks a block of frames
	- RTS/CTS - avoid collisions between clients
- data frames




- Design Guides: https://arubanetworking.hpe.com/techdocs/VSG/
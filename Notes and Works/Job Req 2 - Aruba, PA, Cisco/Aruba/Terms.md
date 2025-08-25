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
- Campus AP (CAP) - AP and the WLC are on the same site
- Instant AP (IAP) - no controller needed. a cluster of APs will elect a Virtual Controller (VC). the VC will push its configs down to the other APs. Generally supports only up to 128 APs
- Aruba Mobility Controller - the WLC for Aruba 
- Controller Hierarchy 
	- Mobility Master (MM) - centralizes the management and control plane. manages mobility controllers
	- Mobility Controllers (MC) - manages the APs. they are Aruba's WLCs
- Airwave - Aruba's on-premises solution for managing and monitoring wireless and wired network infrastructure
- ClearPass - aruba's NAC solution. like cisco ISE
- BSS - the wireless service provided an AP that clients can join
- BSSID - the unique identified for the AP. will be based on the MAC address
- ESS - combo of at least 2 BSS. provides roaming. when the client's signal gets too weak to the AP, it disassociates, then it scans for another AP with the same SSID, once it finds one, it reassociates.
- AirMatch - automatically selects the channels for the APs, optimizes the channel power
- AP Groups - the templates that are assigned to APs. configure them for the controllers. 
- AP Group Auto-Provisioning - when a new AP connects to a controller, it is automatically assigned to an AP group based on rules defined here.
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
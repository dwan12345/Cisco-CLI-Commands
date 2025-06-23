
- include WAPS in HLD?
- What are the considerations for POE
- what requirements are there to connect the financial services proxy (FSP) server to the network? Are there a pair of FSPs?
- are there remote sites or plans for a remote site? should the HLD consider that?
- Should there be an AP in the finance department so that other users can connect wirelessly?

- What is the general size of each room so that I can account for how many APs to purchase?
- To confirm, your connection with Comcast has a LC SM Fiber handoff, and your connection with Century Link has a Copper Ethernet handoff.
- Are there plans to increase the speed of the connection to the ISPs? Otherwise, there is no need to make use of all of the fiber connections. 100 mbps is also way too low for any modern network, so I highly recommend increasing this in the near future.
- Do the DHCP, DNS, Voice Gateway, and FSP servers have NIC cards with ethernet ports or SFP ports?
- Ro confirm, according to the statement of work, your team does require edge firewalls.

- Does your team require me to purchase a VPN concentrator? Is it a physical machine or through the cloud?
- A proper site survey should be conducted to optimize AP placement. Will you be able to provide the site survey? If not, I will place the APs based off of my best judgement and the floorplan.
- Does your team require extra warranties or support plans for the network devices?
- About how many users are there? Include both in-person and remote users.

- For the FSP, are there 2 Palo Alto NGFW 820s? According to the statement of work, there is 1 FSP for each MDF.
- I plan to have 1 WLC in each MDF, working as a HA pair. I will order Cisco WLCs, based on the Statement of Work. Are you comfortable with configuring the HA pair?
- Do you require me to order spare fans and power supplies for the network devices?
- For your IDFs and MDFs, do you prefer port side intake or exit for the fan exhausts? 


- Do you require me to buy UPSs for the networking devices?
- What to do about the ST connections
- Just to make sure, within the IDF, the switches will be placed within the same rack.


















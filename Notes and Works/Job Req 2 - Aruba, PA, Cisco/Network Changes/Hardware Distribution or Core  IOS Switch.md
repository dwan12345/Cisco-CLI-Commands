# Context
- must be distribution or core switches
- must be in HA pair or more


# Requirements
- procure the hardware
- make sure the replacement switch and the remaining switch is the same software version
- ensure the health of all protocols and links
- make sure the remaining switch is able to handle all of the network traffic by itself


# Steps
1. make a backup of the configs. open it in a notepad and shutdown all of the interfaces. this is to ensure that when the new switch is plugged in, it does not immediately interfere with the network. apply the configs to the new switch
2. make the remaining switch the active switch for HSRP for all vlans. then verify
3. make the remaining switch the root bridge for STP for all vlans. then verify
4. for OSPF, make the network prefer routes through the remaining switch. to do this, on the old switch, make the OSPF cost of its port much higher. verify this on the other devices
5. shut down the interfaces on the old switch. ensure that network traffic is flowing properly.
6. unplug and remove the old switch. plug everything into the new switch. 
7. turn on the interfaces one at a time. verify that the protocols turn on and the adjacencies form properly.





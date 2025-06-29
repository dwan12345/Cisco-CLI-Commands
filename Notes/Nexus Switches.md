- high performance switches for data centers
- has a lot of virtualization technology, integrates with cisco ACI





# Services
- Virtual Device Context (VDC) - partitions single nexus switch into multiple logical ones. Used for segregating networks, such as in a cloud environment, or to limit the effects of a failure.
- Create roles and users to have granular control over who can configure what parts of the switch. Can by synced with another AAA service such as RADIUS or TACACS+ server.
- Port profile - create a template for a port which can be applied to many ports. Very scalable. Ensures consistency with ports of the same nature: trunk ports, access ports, server ports. Centralized management. 
- Fabric Extender (FEX) - a FEX extender is a device you buy that has a bunch of ports but no capabilities, only forwards traffic to nexus switch. Connect the device to a nexus switch. The nexus switch will logically have control over all of the ports on the FEX. Used to increase port density, lower port per cost, and efficient management.
- Virtual Port Channel (vPC) - regular etherchannel, but: say 2 nexus switches, 1 server, connect the server to both nexus switches and configure vPC, now it will load balance across both switches and the switches will handle the rest. Without vPC and using 2 regular layer 2 links, STP will block 1 of the ports, which does not allow load balancing.
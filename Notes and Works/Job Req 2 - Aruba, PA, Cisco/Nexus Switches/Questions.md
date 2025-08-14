- tell me about a time you had to troubleshoot vPCs
	- use show commands to collect information. when troubleshooting vPCs, it depends on whether or not the vPC ever worked properly before. If it has never worked, then it is most likely a configuration issue. maybe an inconsistent IP scheme, forgot to use spanning-tree port type network, did not add all of the used vlans into the peer link, MTU mismatch. if the vPC has worked before, then maybe bad cables, a new vlan that was not added to the peer link, a mismatched software version after a recent update. For link errors, check for CRC errors in show interface
- how do you upgrade NX-OS version?
	1. check for any compatibility issues or rolling updates
	2. perform a backup of the current image and the configurations. you can use "checkpoint" but just in case the switch needs a factory reset, backup to an external media
	3. plan out your update strategy
		- upgrade the secondary vPC pair first
		- only upgrade 1 NX-OS at a time
		- verify that vPC links are healthy after each update
	4. download the NX-OS image. verify the checksum
	5. copy into the switch using SCP: copy scp:\<scp IP>/path/to/image bootflash:image.bin
	6. verify the checksum
	7. schedule the downtime
	8. install the upgrade: install all sup-active bootflash:image.bin
	9. verify that everything is working
- **Explain "vPC consistency parameters." What are Type 1 and Type 2 consistency checks, and what happens if there's a mismatch?**  
    - **vPC Consistency Parameters** are specific configuration settings that must be identical on both vPC peer switches for the vPC to function correctly and predictably. These are checked by Cisco Fabric Services (CFS).
    - **Type 1 Consistency (Critical):** Mismatches in these parameters are **critical** and will cause the vPC member ports to be **suspended** (shut down) on the secondary vPC peer (or potentially both, depending on the parameter and NX-OS version) to prevent forwarding inconsistencies, loops, or traffic blackholing. Examples include:
        - switchport mode (access/trunk)
        - port-channel mode (active/on)
        - switchport trunk allowed vlan (if not identical)
        - STP mode, STP port type, bridge priority
        - MTU settings
    - **Type 2 Consistency (Non-Critical):** Mismatches in these parameters are **non-critical** and typically **do not cause ports to be suspended**. However, they can lead to undesirable behavior, asymmetric forwarding, or inefficient load balancing. Examples include:
        - port-channel load-balance method
        - QoS policies
    - You can check consistency with show vpc consistency-parameters global and show vpc consistency-parameters interface port-channel.
- **What is the spanning-tree port type network command used for, especially on the vPC peer-link?**  
    - The spanning-tree port type network command is applied to an interface that connects to another switch or network device.
    - **Purpose on Peer-Link:** On the vPC peer-link, this command is **critical**. It tells STP that the peer-link is a connection between network devices. This helps STP treat the peer-link as a dedicated network link rather than a simple endpoint. It ensures BPDUs are exchanged correctly between the vPC peers, allowing the vPC pair to appear as a single logical STP root to the rest of the network, preventing the peer-link from being unnecessarily blocked by STP and ensuring proper BUM traffic flow.
- 



- "What are the critical pre-checks you would perform before initiating an NX-OS upgrade? Why are these important?"
- "How would you back up the existing configuration and image on a Nexus switch before an upgrade? What's your rollback plan if the upgrade fails?"
- "What is ISSU, and when is it applicable on Nexus switches? Describe the high-level process of performing an ISSU."
    
- "What are the prerequisites for a successful ISSU? What conditions or configurations might prevent an ISSU, forcing a disruptive upgrade?"
    
- "How do you verify the progress and success of an ISSU? What troubleshooting steps would you take if an ISSU gets stuck or fails?"
- "What is ISSU, and when is it applicable on Nexus switches? Describe the high-level process of performing an ISSU."
    
- "What are the prerequisites for a successful ISSU? What conditions or configurations might prevent an ISSU, forcing a disruptive upgrade?"
    
- "How do you verify the progress and success of an ISSU? What troubleshooting steps would you take if an ISSU gets stuck or fails?"
- "You need to upgrade the NX-OS on a pair of Nexus switches configured in a vPC domain. How would you plan this upgrade to minimize downtime and ensure continuous traffic flow?"
    
- "What are the specific steps you would take to upgrade each vPC peer? What potential pitfalls or issues should you be aware of during this process?"




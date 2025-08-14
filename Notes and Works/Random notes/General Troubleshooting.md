1. Identify the problem
	- what exactly is broken?
	- what is the expected behavior, how to replicate the issue, when did it start
	- did it work in the first place, or did it never work to begin with?
2. establish a theory of probable cause
	- narrow the scope of the issue. where is the traffic getting dropped? is it just a subnet? 
	- walk through the path the traffic would traffic to check everything
	- use tracert
	- check the logs
	- confirm the configurations
	- maybe packet capture
3. test the theory
4. establish a plan of action, then implement
5. verify the problem has been solved
6. document findings, actions, outcomes


When you're reading these case studies, pay attention to:

- **The initial symptoms:** How was the problem first identified?
    
- **The troubleshooting methodology:** What steps did the engineers take? Did they follow a systematic approach (e.g., top-down, bottom-up)?
    
- **The tools used:** Which commands, software, or hardware tools were essential for diagnosis? (e.g., ping, traceroute, nslookup, Wireshark, tcpdump)
    
- **The root cause:** What was the underlying issue?
    
- **The resolution:** How was the problem fixed?
    
- **Lessons learned:** What insights did the engineers gain from the experience?



# Scenarios
## The Problem: Partial Network Outage

- **Symptoms:** A segment of a large office couldn't access the internet or external applications.
- **Initial Checks (Seemingly Normal):**
    - **Client Connectivity:** Clients appeared to have valid IP addresses, subnet masks, and default gateways.
    - **Layer 2 (ARP/MAC Tables):** The switches "saw" the client's MAC addresses, and the clients had ARP entries for their default gateway (meaning they knew its MAC address). Crucially, the gateway also had ARP entries for the clients. This suggested Layer 2 connectivity should have been working.
### The Misleading Troubleshooting Attempts
- **Rebooting Everything:** Switches and clients were rebooted, a common troubleshooting step, but ineffective here. This indicates the problem wasn't a transient software glitch or a simple ARP cache issue.
- **Lack of Obvious Clues:** The "usual data and standard steps" didn't immediately reveal the core problem, leading to frustration. This suggests the issue was subtle and perhaps not immediately apparent in standard output.
### The Root Cause: A Static MAC Address Entry and Bridged Ports
The key revelation:
- **Static MAC Address Entry for Default Gateway:** The crucial clue was that the MAC address of the default gateway (which is typically a router or firewall) was configured as **STATIC** in the switch stack's MAC address table.
    - **Why is this bad?** Normally, MAC addresses are dynamically learned by switches. If a switch learns a MAC address on a specific port, it assumes that device is connected there. If the device moves, or if there's an issue, the switch eventually ages out the old entry and learns the new one. A static entry forces the switch to believe a MAC address is always on a particular port, regardless of where it actually is.
- **"Bouncing Between Ports":** This implies that the gateway's MAC address was being seen on multiple ports, but the static entry was overriding the dynamic learning or causing confusion. The "bouncing" behavior (seeing the MAC on different ports) should have been a major red flag, as a single MAC address should only be seen on one physical port at a time, unless it's on a trunk/port-channel.
- **End User Bridged Two Ports:** This is the critical user error. An end-user physically connected two different access ports on the switch (or the same switch stack) with an Ethernet cable. This creates a **Layer 2 loop**.
- **Port Security/Sticky MAC:** One of the bridged ports had "port-security" or "sticky MAC" configured.
    - **Port Security:** This feature restricts the number of MAC addresses learned on a port and can "stick" a MAC address to a port.
    - **How it contributed:** When the user bridged the ports, the switch saw the gateway's MAC address (and potentially other network devices' MACs) on this new, unauthorized port where the user connected their cable. Because of sticky MAC, the switch permanently learned (or "stuck") the gateway's MAC to this user's access port.
### The "Black Hole" Effect: How it Caused the Outage
- **Incorrect Forwarding:** When the switch stack received traffic destined for the default gateway's MAC address (from the affected clients), it looked up its MAC address table. Since the gateway's MAC was **statically pinned to the user's "bridged" access port** (due to the sticky MAC/port security interaction), the switch would forward all traffic for the gateway to that specific port.
- **No Gateway Present:** The default gateway (router/firewall) was not actually connected to that user's port. Instead, it was connected to a legitimate uplink port elsewhere in the network.
- **Traffic Black Hole:** Consequently, any traffic from the affected clients trying to reach the default gateway was sent to the user's bridged port and effectively **disappeared** (black-holed) because there was no device on that port to receive it and forward it. The gateway never received the clients' traffic, and thus couldn't respond.
### Isolating the Issue
- **Affected User Pool:** The crucial troubleshooting step that led to the solution was identifying that not all users were affected. By finding a group of affected users and tracing where they were plugged in, the network team could isolate the problem to a specific switch stack. This is a vital diagnostic technique to narrow down the scope of a problem in a large network.
### Key Takeaways and Lessons Learned:
- **Layer 2 Issues are Tricky:** This scenario exemplifies how Layer 2 problems, especially those involving MAC address tables, loops, and port security features, can be very difficult to diagnose because lower-level checks (like ARP) might appear normal.
- **Static MAC Entries are Dangerous (Generally):** Unless there's an extremely specific and controlled reason, relying on dynamically learned MAC addresses is almost always preferred. Static entries can cause significant issues if not managed meticulously.
- **Port Security is a Double-Edged Sword:** While valuable for preventing unauthorized devices and MAC spoofing, improper configuration or interaction with user errors (like bridging ports) can lead to unexpected outages.
- **Loops are Network Killers:** Bridging ports creates a Layer 2 loop, which can rapidly consume bandwidth and destabilize an entire network by causing MAC address table instability and broadcast storms. Spanning Tree Protocol (STP) is designed to prevent these, but certain configurations or misconfigurations can bypass or interfere with it.
- **"Bouncing MACs" is a Critical Symptom:** Seeing a MAC address constantly appearing on different ports is a strong indicator of a Layer 2 loop or misconfiguration.
- **Systematic Isolation is Key:** The ability to isolate the problem to a specific switch stack by identifying affected users was crucial to eventually finding the root cause.

## Another Scenario




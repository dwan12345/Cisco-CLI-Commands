# CIA
- Confidentiality - only authorized users should be able to access the data.
- Integrity - data should not be tampered with by authorized users. Data should be correct and and authentic.
- Availability - network and services should be accessible to authorized users.

# Random Definitions
- Vulnerability - a potential weakness. It is not necessarily a problem.
- Exploit - something that can be used to exploit a vulnerability. 
- Threat - the potential of a vulnerability to be exploited. 
- Mitigation technique - something that can protect from threats.

# Attacks
- DoS - denial of service. attacks the Availability of CIA. 
	- SYN ACK attack: exploits TCP 3 way handshake. Attacker sends SYN, server responds with SYN ACK, attacker does not respond with ACK. This fills up TCP connection table of server.
- DDoS - DoS but with a lot of computers. Usually a botnet
- Spoof - uses fake source IP, MAC address, etc.
	- DHCP Exhaustion - attacker spoofs MAC address to flood DHCP discover messaged. DHCP responds with Offer message, so they will not offer that IP to other hosts. The DHCP pool fills up. Attacks Availability
	- Reflection/Amplification Attack - attacker sends traffic to a reflector (ie DNS or NTP server), the source IP is spoofed to attack target so the reflector responds back to attack target. If the reflector responds with large amount of traffic, it is an amplification attack. Attacks Availability
	- ARP Poisoning - during ARP process for a server or DFG, attacker responds back with his MAC address for the IP. Now people send traffic to the attacker when they are accessing the server or DFG. The attacker forwards the traffic to the real destination and forwards the response back. Attacks confidentiality and integrity
- Reconnaissance Attacks - gather info about target for potential vulnerabilities. nmap. Not really an attack by itself
- Malware - harmful software
- Virus - requires host program. 
- Worms - does not require host software to propagate. Can spread without user interaction.
- Trojan horse - malware disguised as legitimate software.
- Social Engineering - target the people
	- Phishing - fraudulent emails that looks legitamate
		- Spear phishing - target a specific group of people, such as people that work at a bank
		- whaling - target high profile individuals
		- Vishing - phishing over the phone
		- Smishing - SMS text messages
	- Watering Hole - compromise a website that a specific group of people usually visit. Those people trusts that website, so they will not hesitate to click links and stuff
	- Tailgating - entering restricted area behind an authorized person.
- Password related:
	- Guess the password
	- Dictionary - attackers uses a large list of common passwords to guess the password
	- brute force - try every combo of password

# AAA
- Authentication - verify the user's identity
- Authorization - granting user the appropriate permissions
- Accounting - logging the user's events
- enterprises usually use a AAA server
	- RADIUS
	- TACACS+
- Cisco ISE - cisco's AAA server

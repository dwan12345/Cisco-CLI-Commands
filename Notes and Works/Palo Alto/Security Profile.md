- after your security policies have allowed the traffic, security profiles scans it again for specific threats. profiles are configured within a policy
- Examples:
	- Antivirus - uses signatures
	- anti spyware - uses signatures
	- vulnerability protection
	- URL filtering - control access to websites based on their types, such as gambling.
	- file blocking - block certain file types such as exe, zips
	- WildFire Analysis
	- data filtering - DLP (Data loss prevention). 
	- DoS Protection - no default profile. configure max connections/seconds before shutting off connection. Aggregate type means to count all traffic. classified type means to count only traffic that matches rules, such as source and dest IP/zone.
- default security profiles are provided, but you can configure your own
- the profiles match against signatures, then take an action according to the configuration. the action can be changed 
- you can configure exceptions to security profiles

# Configuration
- to create security profiles: objects -> security profiles 
- security profiles are enabled via the security policies
	1. policies -> *click on your policy* -> actions
	2. change "profile type" to "profiles"
	3. enable whichever profile you want

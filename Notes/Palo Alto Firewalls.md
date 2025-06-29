- Panorama - a device that you buy to centrally manage multiple firewalls. Recommended for 6+ firewalls.


# Layer 3
- Security policy - a set of rules with corresponding actions. Traffic is matched with first rule, then action is taken on that traffic. If no matches, implicit deny. The action can be block, allow, log this traffic, use threat prevention
- Zones - group of interfaces that share a common security policy, can be virtual interfaces. Example zones: DMZ, Untrust, Trust, Wireless.
- Virtual router - a PA firewall can have several logical routers that are independent of each other. Example use case would be different virtual router for each department, if you are CSP, virtual router for each customer. There is always at least the virtual router called "default"
- 
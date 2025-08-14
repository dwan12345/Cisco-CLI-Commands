
# Edge Firewalls
1. assign private IPs to the new firewalls
2. start configuring the new firewalls and moving over the configurations while the old firewalls are still operating normally
3. after the configurations are moved over, configure the routing of the internal network to move traffic over to the new firewalls, also make sure the edge router routes the return traffic to the new firewalls as well.
4. if it works, great. if something breaks, change the routing back to forward the traffic to the old firewalls.
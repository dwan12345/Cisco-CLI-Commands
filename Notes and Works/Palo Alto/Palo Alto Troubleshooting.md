- make sure the problem is with the firewall, it could be with anything in the network
	- review firewall logs to see if the traffic is getting dropped or permitted
	- do trace route to see if it is getting past the firewall
- 



# Logs
- use the logs at monitor -> logs -> traffic
	- filter the logs based on source IP, destination IP, and port. you can click on the links to automatically add them to the filter
	- find the destination IP of a domain using: nslookup \<domain name>
	- look at the deny/allow column along with the rule associated with the action
- if a certain rule (security policy) is discovered to be causing issues, you can create a new rule right above the rule causing the issue. the new rule would patch the issue
- there are various other logs such as URL filtering, threats, data filtering, etc.

# Packet Capture
- monitor -> packet capture
- add filtering to capture based on source and destination IP. make sure to add the reverse as well. you can also do the interfaces
- make sure to configure capturing
	- add the drop, receive, transmit, and firewall stage
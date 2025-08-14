- uses DNS to load balance
- the F5 GTM becomes an authoritative DNS server for the domain name, meaning that ISPs' DNS servers will contact our GTM to resolve our domain if they do not have it cached
- load balances across many virtual servers/data centers.

# Traffic Flow
1. client types "example.com" into browser.
2. client contacts ISP's DNS server
3. ISP's DNS server our GTM to resolve our domain
4. Our GTM receives the DNS request and sees that it came from the ISP's DNS server
5. Our GTM makes an intelligent decision, maybe based off of the location of the ISP's DNS server, and responds back with one of our data centers that is closest to the ISP. The IP of the VS of that data center is returned.
6. ISP's DNS server forwards the IP of the VS to the client.
7. The client reaches their closest data center.


# Basic Configuration
- Must have at least 2 F5s with LTM virtual servers already configured
- Create the Data centers
	1. DNS -> GSLB -> data center list -> create
	2. name it
- Create the servers
	1. DNS -> GSLB -> server list -> create
	2. name it
	3. select the data center
	4. For Product, select BIG-IP system if its another F5, such as LTM. Select Generic host for everything else. 
	5. add the IP address to reach said device
	6. enable virtual server discovery if the device is a F5. This allows us to automatically discover LTMs that this BIG-IP sees
	7. configure health monitors
	8. finish
- enable iQuery
	- ensure network connectivity
	- the self IP used must allow TCP 4353
	- NTP server must match
	- From one of the BIG-IPs, go into CLI and type: bigip_add \<other LTM IP>
- To verify:
	- the BIG-IPs under server list will have an UP status
	- DNS -> GSLB -> Server List -> *click on your server* -> virtual servers: you should see the virtual servers configured under this LTM
- create a pool
	- select A record for IPv4
	- make sure to add the members: the LTMs, and other servers
- create the wide IP
	- add all the pools
	- add the FQDN
- create listener
	- the listener IP should be a self IP that is already created. The self IP must be reachable by your DNS clients
	- use the default DNS profile
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

# Definitions
- Listeners - listens for the DNS traffic on a specific IP and port (usually 53) that is intended for the GTM
- Wide IP - a FQDN that you want the GTM to manage. Pretty much like an A or AAAA record. 
- Pool - a group of virtual servers. Associated with a single data center. The Wide IP chooses which pool/data center to tell the user to use, then the pool/data center load balances across its virtual servers.
- Virtual Server (GTM Context) - essentially a virtual server in the LTM
- Data Center - an object that represents a data center. This object contains the pools. You define the geographic characteristics of the data center.
- iQuery - how geographically different GTMs and LTMs communicate with each other. trust must be established between the devices
- Synchronization Group - group of GTMs that sync their configs and operate in HA
- Dynamic Load Balancing
	- Completion Rate - measured in number of connections that were opened, processed, and closed properly.
	- Round Trip Time (RTT) - lowest latency from a data center. Measured from the data center to the local DNS server of the client
	- Topology - goes to nearest data center
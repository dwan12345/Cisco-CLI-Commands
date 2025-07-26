- this is a linux tool to capture packets going in or out of an interface. 
- just prints traffic in the CLI, but can store captured traffic in binaries, which can be analyzed by wireshark

# Command
- run in CLI of F5
- tcpdump -i 1.1
	- captures traffic from interface 1.1
- tcpdump -i 1.1 -w /var/temp/MYCAPTURE.pcap
	- saves the capture in a file, which can be downloaded and opened in wireshark
	- use ctrl+c to stop packet capture
	- use WinSCP to extract the file
- tcpdump -i 0.0
	- capture traffic from all interfaces
- tcpdump -i 0.0 host \<virtual server outside IP\> and port \<port num>
	- the IP above is a virtual server. This captures all traffic going through that virtual server
- tcpdump -i 0.0 host \<client IP> and host \<virtual server outside IP
	- captures specific traffic only from a certain client to a certain virtual server.
- tcpdump -nni 0.0:nnnp -s0 -c 10000 -w /var/temp/capture_$(date +%Y%m%d%H%M).pcap host \<client IP> and host \<virtual server IP> and port \<port num>
	- a tcp command to run in production environment
	- -nn disables hostname and service name resolution, which disables unnecessary DNS lookups and  
	- :nnn adds detailed F5 info to each packet, which includes virtual server name, pool member IP, TMM instance. makes wireshark analyses very insightful
	- :p captures the packets that fit our filter and the corresponding packets on the other end of F5's full proxy. gives us a better picture of the entire flow
	- -s0 captures the entire packet to see the full packet headers and payload
	- -c limits the number of packets
	- $(date +%Y%m%d%H%M) stores the file in YYYYMMDDHHMM format

 
- do not assume, verify
- use other tools before using wireshark

# Scenarios
- we are unable to access our FTP server that is running on our windows server. our packet capture has reset messages immediately after sending out the syn. this means that the FTP server is not running
	- lets say our tcp 3 way handshake completes. but a fin-ack is immediately send by the server. this is not a network issue, so check the ftp server configs
- in wireshark, a client is talking to a server normally. then only 1 side is talking with no responses from the other, after a while of this, a reset message is sent. 
- firewalls can be configured to send resets in case of suspicious activity. If a server suddenly receives a reset with a TTL that was not subtracted, then it was sent by a firewall

# Command Line Tools
- pckmon: packet capture tool for windows
	- this saves the packet capture in an etl file. to change to a pcap file, use the pckmon options
- netstat -an: windows command for showing established and listening TCP connections. used to check if certain servers are up
- tcp dump: packet capture for linux

# TCP
- verify TCP 3 way handshake
- check if there was a Reset message
	- reset message is used to abruptly terminate the connection or when there is no service running on that port
	- this message is sent if a sever receives a syn message on a closed port. so verify that you are connecting to an active service on the server
	- firewalls can send this message in for suspicious activity. this is not recommended because it tells people that there is a firewall here
- when client sends a syn, but no syn-ack was transferred back
	- firewall drop the syn in case of suspicious activity. this should be the behavior because it does not respond back, meaning no information to the attacker
	- the packet was lost along the way somehow

# Packet TTL
- default TTL is different for each OS
	- windows is 128, linux is 64 or 255
- pings return TTL. The returning TTL is based on the OS of the network device that we are pinging. If we ping a linux with a default of 64, our TTL will be less than 64
	- this can be used to determine how many hops away something is
- when TTL reaches 0, there can be silent drops or replies to tell you that TTL was reached


# Slow Network Troubleshooting
- link level error
	- test the wires
	- look for errors on network devices along the way
	- in trace files, look for retransmissions, dup acks, out of order traffic, discards
- TCP handshake shows round trip time. a long RTT can limit bandwidth
- check PCAPs on both client and server. if there are window full TCP errors, then the window size is not growing for some reason
- 


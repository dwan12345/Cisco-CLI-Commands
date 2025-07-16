
# TFTP
- UDP port 69
- no authentication or encryption
- TFTP Reliability (Lock Step communication):
	1. Server sends data, then waits for ACK
	2. PC sends ACK
	3. If server receives ACK, send next data.
	4. PC has a timer to wait for next data. If ACK is lost, then PC timer goes down, then PC sends ACK again
- TFTP Connection Phases:
	1. Connection: PC sends request to server. Server responds back. Initializes the connection.
	2. Data transfer: does the Lock Step Communication.
	3. Connection termination: after last data packet has been sent, a final ACK is sent to terminate the connection.

# FTP
- usernames and PW are used for authentication, but no encryption
- FTP control connection over TCP 21
- FTP data transfer over TCP 20
- Active mode: the server initiates the data connection.
- Passive mode: the client initiate the data connection. Necessary when client is behind firewall because firewall blocks server data connection initiation. 




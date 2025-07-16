# Frame
- Preamble -> Start Frame Delimiter -> Ethernet Header -> Payload -> Frame Check Sequence

## Preamble
- 7 Bytes
- Made up of alternating 1s and 0s: 101010...
- Helps receiving device synchronize its clock with the incoming data stream.

## Start Frame Delimiter
- 1 byte
- Unique byte pattern of 10101011
- signals the end of the preamble and the beginning of the actual ethernet frame

## Ethernet Header
- 14 bytes: 6 for destination mac, 6 for source mac, 2 for the type
- Type: signifies which IP protocol it is using, usually IPv4 (0x0800), ARP (0x806), and IPv6 (0x86DD)

## Payload
- The minimum payload is 46 bytes
	- The actual minimum is 64 bytes including the header and Frame Check Delimiter
	- The reason is because in old days, there was only half duplex. We need to make sure that the device did not finish sending the frame before the detecting the collision.
- padding 0s are added if less than 46 bytes

## Frame Check Sequence (FCS)
- 4 bytes
- Contains Cyclic Redundancy Check (CRC): calculated from the ethernet frame, excluding the preamble and start frame delimited, which the end device can calculate too in order to check for errors



# IPv4
- version -> IHL -> DSCP -> ECN -> total length -> ID -> flags -> fragment offset -> TTL -> protocol -> header checksum -> source IP -> destination IP -> options -> payload
## Version
- 4 bits
- 0100 for IPv4, 0110 for IPv6
## Internet Header Length (IHL)
- 4 bits
- to indicate the total length of the header (in 4 byte increments) since the options field is variable in length
- minimum value in this header is 5, meaning 20 bytes header, which means the options field is empty
- maximum value is 15, meaning 60 bytes header 
## Differentiated Services Code Point (DSCP)
- 6 bits
- for QoS purposes, prioritize voice and video for example
## Explicit Congestion Notification (ECN)
- 2 bits
- notifies of network congestion to endpoints
- optional field that requires both endpoints to support it
## Total Length
- 16 bits
- the total length of packet including the header and payload
- measured in bytes
## ID
- 16 bits
- for when packets are fragmented, this field is used to identify which packet it belongs to
- packets are fragmented if larger than the MTU, which is usually 1500 bytes
## Flags
- 3 bits
- used to control fragmentation behavior
	- first bit: always 0
	- second bit: if set, do not fragment packet
	- third bit: set to 1 if there are more fragments, set to 0 for last fragment
## Fragment Offset Field
- 13 bits
- indicate the position of the fragment within the original IP packet
- used so that even if packets arrive out of order, they can be reassembled
## TTL
- 8 bits
- self explainable
## Protocol
- 8 bits
- indicates the transport layer protocol being used
	- TCP: 6
	- UDP: 17
	- ICMP: 1
	- OSPF: 89
## Header Checksum
- 16 bits
- checksum only for the header part
- The payload is checked by TCP/UDP
## Source IP and Destination IP
- self explanatory
## Options
- 0-320 bits
- rarely used, usually empty

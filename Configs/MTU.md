- Maximum transmissible unit
- There are ethernet MTUs and IP MTUs
- Default MTU is 1500 bytes
- Larger MTU increases network efficiency by increasing the data to header ratio
- larger MTU can increase network delay, more susceptible to packet corruption, more time to retransmit packet, 
- Jumbo frames - frames larger than 1500 bytes
- MTU must match 
- GRE tunnels add on an extra 24 bytes, so the MTU of the tunnel interface should be 24 bytes lower than the outgoing interface's MTU to avoid fragmentation.

# Ethernet MTU
- The maximum size of the PAYLOAD in an ethernet frame, so it includes the IP header, TCP header, data, but not the ethernet header and trailer
- will drop frame greater than MTU
- Size of frame from 64-1522 bytes
	- 64 is the minimum, will add padding 0s to reach 64
	- 1518 is with ethernet header and trailer
	- 1522 is 1518 plus 4 from the dot1q tag

# IP MTU
- Maximum size of an IP packet before it must be fragmented
- packets bigger than MTU are fragmented. There is DF bit in IP header, if set, it will drop packets larger than the MTU
- Cannot be greater than ethernet MTU
- when ethernet MTU is increased, IP MTU is automatically increased



```js
! change the MTU
conf t
int [interface]
mtu [bytes]
ip mtu [bytes]
end
```



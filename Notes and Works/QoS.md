- traditional phones use Public Switched Telephone Network (PSTN)
- VOIP uses traditional IP network
- Power policing - during POE, the port monitors the power provided to the device to ensure it does not draw too much power. 

# What QoS Manages
- Bandwidth: save 25% of the bandwidth of a link for voice, leave the rest for everything else. 
- Delay: the latency. One way delay should be less than 150 ms
- Jitter: the variation in one way delay between packets sent. 30 ms or less
	- IP phones have a buffer of packets to provide consistent delay between each packet
- Loss: packet loss rate. 1% or less

# Queues
- Each class of data (voice, data, wireless, etc) has a queue
- Round Robin: take 1 from each queue, repeat
- Weight Round Robin: more is taken from high priority queues.
- Class based weighted fair queueing (CBWFQ):  weighted round robin, but guarantees each queue a certain percentage of bandwidth during congestion 
- Round robin is not ideal for voice and video because it can add jitter
- Low latency queueing (LLQ): will always take from the lowest queue, that has traffic in the buffer, until it is empty. best for voice and video. Downside of starving other queues

# Traffic Shaping and Policing
- Shaping: buffers traffic in a queue if the traffic goes over the configured rate
- Policing: drops traffic if the traffic rate goes over the configured rate
	- Burst traffic can be buffered for only a short period of time
- policing can be used by ISP on inbound connection from customer to not go over what the customer bought
- shaping used by customer outbound to ISP because if they go over their limit, they know it will be dropped, so best buffer it

# POE
- Cisco Inline Power (ILP) - the first POE made by cisco. 7 watts
- POE - 15 watts
- POE+ - 30 watts
- UPOE - 60 watts
- UPOE+ - 100 watts
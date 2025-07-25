- an HA mechanism to make failover quick and seemless
- Active RP (Router Processor) - handles all control plane functions such as configuration management, STP, etherchannel, port security, etc. 
- Passive RP - syncs its layer 2 protocols with the active RP, a process called checkpointing. Can take over in 0-3 seconds. Layer 2 forwarding does not flap, but layer 3 does because layer 3 adjacencies go down. 
```js
! enable SSO
conf t
redundancy
	mode sso
	end
```

```js
! show commands
show redundancy
```

# Non-Stop Forwarding (NSF)
- allows line cards to continue to forward L3 packets when failover happens
- enabled by default when SSO is enabled
- Essentially: the FIB is transferred from the active RP to the passive RP, then it is updated when there are changes. 
- routing protocols are still interrupted, meaning that upstream devices will lose routes to the downstream network. This is solved with GR

# Graceful Restart (GR)
- requires neighbors to peer
- even when routing protocols goes down, GR neighbor devices will continue to maintain the routing table. 
- Grace period - the period of time for which the GR neighbors will forward traffic.
- GR capable - capable of failing while performing GR
- GR aware - able to peer with a GR capable, and continue forwarding while GR capable device reboots

# Non-Stop Routing (NSR)
- NSR maintains neighbor routing protocol neighbor adjacencies during RP failover
- does not require neighbors to peer
- along with the FIB, routing protocol adjacencies are also checkpointed

- allows multiple VLANs to be assigned to a single STP instance, which reduces the number of BPDUs sent and the processing of STP
- its underlying tech is RSTP, so it basically operates the same
- MST Instance (MSTI) - the STP instance for which you assign multiple vlans to. say you have 2 distribution switches, which you want to be the root bridges. you will have 2 MSTIs, where half of your VLANs are assign to 1 MSTI and the other half to the other MSTI
- MSTI 0 is created by default and it is special
	- all vlans not assigned to another MSTI is assign to MSTI 0 so that all vlans can at least communicate
	- acts as the representative of the MST region when communicated to other STP protocols
	- only this MSTI sends BPDUs
- 


# Commands
```js
! enable MSTP
conf t
spanning-tree mode mst
end
```

```js
! change MSTP priority
conf t
spanning-tree mst <instance num> priority <priority>
end
```

```js
! map VLANs to an MST instance
conf t
spanning-tree mst config
instance <instance num> vlan <vlan range>
end
```

```js
! configure port cost or priority
conf t
int <interface>
spanning-tree mst <instance num> cost <cost>
spanning-tree mst <instance num> port-priority <priority>
end
```

- you cannot set different timers for each MSTI because only MSTI 0 sends out BPDUs
```js
! configure hello, forward, max age times
conf t
spanning-tree mst hello-time <seconds>
spanning-tree mst forward-time <seconds>
spanning-tree mst max-age <seconds>
end
```
# Show
```js
show spanning-tree mst
show spanning-tree mst configuration
show spanning-tree mst interface <interface>
```



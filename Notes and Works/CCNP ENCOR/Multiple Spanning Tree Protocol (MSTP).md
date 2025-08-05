- allows multiple VLANs to be assigned to a single STP instance, which reduces the number of BPDUs sent and the processing of STP
- its underlying tech is RSTP, so it basically operates the same
- MST Instance (MSTI) - the STP instance for which you assign multiple vlans to. say you have 2 distribution switches, which you want to be the root bridges. you will have 2 MSTIs, where half of your VLANs are assign to 1 MSTI and the other half to the other MSTI
- MSTI 0 is created by default and it is special
	- all vlans not assigned to another MSTI is assign to MSTI 0 so that all vlans can at least communicate
	- acts as the representative of the MST region when communicated to other STP protocols
	- only this MSTI sends BPDUs
- Regions - each region logically runs its own MSTP. it has its own IST.
- Internal Spanning Tree (IST) - within a region, any vlans not part of another MSTI will be assigned to the IST. This is also referred to as MSTI 0
- Common Spanning Tree (CST) - when different regions connect to each other, the entire region is treated as a single switch. This topology is called the CST. It also includes switches with other STP protocols.
	- the root bridge is determined by the region with the bridge that has the best BID
	- root port is based on lowest path cost to the root region. If tied, then the lowest BID of the non-designated region's switch
- Common and Internal Spanning Tree (CIST) - combination of the CST and IST.
- Region name - the name must match for switches to be in the same region
- Revision number - default 0. the revision number must match for switches to be in the same region. Kind of useless because we can just use region name


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

```js
! configure MSTP region name and revision number
conf t
spanning-tree mst config
name <region name>
revision <num>
end
```



# Show
```js
show spanning-tree mst
show spanning-tree mst configuration
show spanning-tree mst interface <interface>
```



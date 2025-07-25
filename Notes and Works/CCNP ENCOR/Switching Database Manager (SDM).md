- allows you to manage how much TCAM is allocated, such as for MAC forwarding, L3 forwarding, ACLs.
- Since TCAM is finite, if it overflows, then certain unwanted behavior may occur
	- using CPU for L3 forwarding and ACL
	- flooding frames when MAC address TCAM is full

# SDM Templates
- templates for how much is allocated to each resource. There are prebuilt templates, and only some devices support custom templates. the prebuilt templates also depend on the specific switch
- example templates
	- Default template: a balance of all functions
	- Access template: more for ACLs
	- VLAN template: all in on VLANs and MAC forwarding, only use for pure layer 2 switches
- some templates do not allocate any resource for IPv6. If this is the case, then IPv6 will not even show up in the list of commands

# Commands
- show current template
```js
show sdm prefer
```
- use a template. this does not take effect immediately. On next reload, this will be applied
```js
conf t
sdm prefer <template name>
end
```
- show current tcam utilization
```js
show platform tcam utilization
```
- 
```js

```






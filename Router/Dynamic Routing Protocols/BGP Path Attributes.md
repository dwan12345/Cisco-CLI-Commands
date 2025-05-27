
## Show
- Most path attributes can be seen in show command below
```js
show ip bgp 
```

## Path Attributes
- Weight: cisco proprietary, higher weight is preferred. Usually used for outbound routing decisions. Locally significant, meaning that it is not advertised to other routers. Usually used to set the weight for inbound routes, which will influence outbound routing decisions. Default is 0
```js
conf t
ip prefix-list <prefix list name> seq <sequence num> <permit | deny> <network ip/mask>
route-map <route map name> <permit | deny> <sequence num>
	match ip address prefix-list <prefix list name>
	set weight <weight value>
	exit
router bgp <AS num> 
	nieghbor <neighbor IP> route-map <route map name> in
	end
```
- Local preference: higher is preferred, spread throughout the AS. Used to influence outbound communications. default is 100. Configured the same as weight.
- Originate: paths that are connected are preferred
- AS path length: how many AS the path to a network is. Lower is preferred. Usually used to influence inbound routing decisions. By prepending your own AS number, you can artificially increase the AS path length to get to your own routes.
```js
conf t
route-map <route map name> permit <seq num>
	match ip address prefix-list <prefix list name>
	set as-path prepend <AS num> <AS num> <AS num>
	exit
router bgp <AS num> 
	nieghbor <neighbor IP> route-map <route map name> out
	end
```
- Origin type: how the route was injected into BGP. Show in BGP table. "i" means a network command. "e" means EGP, we will never see this. "?" is redistributed. The preference is i, e, ?. 
- Multi-exit discriminator (MED): lower MED is preferred. Attach MED number to outbound routes to influence how they will route to you. Used to influence how adjacent ASs select an entry point into your AS when there are multiple paths to your AS from the same adjacent external AS. To configure, same as weight but uses "set metric"
- Paths: prefer eBGP over iBGP
- Router ID: lowest router ID is preferred



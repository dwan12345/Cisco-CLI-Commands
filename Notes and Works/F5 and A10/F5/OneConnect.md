- F5 OneConnect - LTMs operate as a full proxy, meaning that it maintains 2 independent connections, 1 to the client, 1 to the server. 
	- Problem to solve: a new TCP connection needs to be established for each distinct request. this is processor intensive. By default, the load balancer will send all client requests to a specific server instead of spreading it out.
	- Solution: have a reuse pool of idle TCP connections that the LTM will use, so new TCP connections do not need to be established. Now the load balancer can spread out the user requests to many servers.
- F5 needs SSL offloading for OneConnect to work properly
- OneConnect should be used with caution if not using HTTP
- VS must be assigned HTTP profile along with OneConnect Profile
- do not use source IP persistence, since with SNAT, they can appear to be the same client, which ruins load balancing
- do not use on stateful applications
- create OneConnect Profile
	1. local traffic -> policies -> other -> OneConnect -> create
	2. parent profile of "oneconnect"
	3. Finish
- Apply profile to VS
	1. local traffic -> virtual servers -> *click on your VS*
	2. make sure it has an HTTP profile
	3. scroll down to se OneConnect, apply the profile we created



HA cluster





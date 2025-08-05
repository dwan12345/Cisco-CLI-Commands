- Pool - logical grouping of multiple servers. What the F5 will be load balancing across.
- Node - the actual server. Needs to have a physical or virtual IP address. Can only be used when added to a pool
- profiles can be applied to pools and nodes
- priority groups within pools can be configured
- health checks are applied on nodes
# Create Nodes
- main -> local traffic -> nodes -> create
- Add name, description, IP, health monitors, ratio, connection limit, connection rate limit
	- ratio: the weight used in weighted load balancing strategies. 1 is default
- 
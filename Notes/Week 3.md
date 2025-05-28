
# Cloud

	
	
- COLO: colocation. hardware owned by company , self managed
- Virtualization: hardware is divided into different computers. hypervisor is software to fun multiple VMs into single machine
- Type 1 hypervisor: bare metal. Software installed directly on the physical computer. It interacts directly with the physical hardware
- Type 2 hypervisor: hosted, software installed as an app on the computer.
- hypervisor/virtualization good because you can make use of pc resources that is not currently used
- Cloud computing - on demand delivery of IT resources with pay as you go pricing. 
- Advantages: 
	- variable expense instead of huge up front cost
	- Economies of scale from CSP
	- Elasticity
	- deployment time
	- no physical hardware to manage
	- globally available
	- automation
- Disadvantage:
	- security: less control over your data, always online
	- cost: unexpected cost, it can be more expensive
	- requires internet activity
- Types of Cloud computing:
	- SaaS - completed product, end user application, gmail, office 365
	- PaaS - platform as a service. Do not manage underlying infrastructure, but you develop the applications
	- IaaS - service provider does the hardware, customer controls resource utilization, apps, etc.
![[Pasted image 20250528095443.png]]
- Deployment types
	- public cloud - everything on CSP. available to the public. cheaper, less secure
	- hybrid cloud - interconnected between public and private. more difficult to manage
	- private cloud - deploying on premises, then using virtualization. most secure and expensive, do not share with other customers
	- community cloud - only select organizations. more secure than public. less scalable
	- multi-cloud - uses multiple public clouds. highest availability. highest complexity
- Regions
	- each region is completely independent
	- not all services in the same region
	- can host data and services in multiple regions
	- each region has at least 2 availability zones
- availability zones
	- 1 or more data centers owned by CSP
	- each have redundant power, networking, connectivity
	- physically separate from other AZs
	- independent failures
	- connected via low latency links to other AZs
- local zones
	- place servers closer to users
	- useful for low latency and high bandwidth apps for users, or places with higher demand
- AVs are within regions. local zones are offshoots off of regions
- Cloud services
	- DNS - domain name registration. health checkings, DNS services
	- CDN - content delivery network. Cache content near users to lower latency and increase reliability
	- Storage - used for storage in AWS. persistent and reliable data. Essentially unlimited storage.
	- load balancing - auto distributes across multiple targets. Can load balance across multiple AVs
- EC2 instance - virtual, elastic things
- Pricing
	- based on usage
	- Most cost savings are from removing unused resources
	- EC2 instances have specialized pricing: on demand, reserved, spot, 
	- use CSP price calculators

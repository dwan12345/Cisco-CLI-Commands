
# Module 2
1. To explain the general traffic flow, lets start from the user using the DNS name of the load balancer.
2. We type the DNS name into our browser, which will get resolved by whatever DNS server we are connected to. This is handled by Amazon.
3. Our traffic will be routed to our VPC and hit our internet gateway.
4. It will be forwarded to our Application Load Balancer.
5. The Load Balancer will use the target group to pick which EC2 instance it will send the traffic to.
6. The EC2 instance will receive the traffic and respond appropriately based on its security group policies.

# Module 3 Part 1
1. Lets start from the top.
2. Route 53 is used to register the domain name along with handling DNS queries. It also provides health checks on our EC2 instances to make sure it does not route traffic to bad instances. We can use it to perform latency based and geolocation based routing. Route 53 will effectively never go down because AWS has a 100% uptime SLA.
3. The application load balancer will be used to load balance among our EC2 instances. It also ensures HA by load balancing across multiple AVs. 
4. Auto scaling group will be used to scale up and down the number of EC2 instances we have to meet traffic demand but also keep costs low. 
5. The instance type we will be using is the t4g.small because it provides 2 vCPUs and 2 gb of RAM, which are above the minimum amount.
6. For our databases, we have them in a private gateway so that they cannot be confined and so that they cannot be accessed directly from the internet.
7. Aurora is used because it is a managed relational database service, meaning that SIC can focus on using the database instead of managing it. Aurora automatically provides HA granted that we have created a replica in another AV. Aurora Serverless is used so that it automatically scales up and down the performance based on network traffic. The computing power of Aurora is measured in Aurora Capacity Units, where 1 ACU is roughly equivalent to 2 vCPU and 2 gigs of RAM, so for this case, we will set a minimum ACU of 1 and maximum of 4. Aurora also provides capabilities to move data in and out of the database: S3, AWS Database Migration service, up to your choice.
8. The NAT gateway is needed to allow Aurora to initiate a connection to the outside. This can be for various reasons such as saving data is an S3, sending health metrics, or saving a backup somewhere else. 
9. I chose to use Business support because it offers fast response times from the Amazon Support team and many other support services, but is not as expensive as enterprise support.


# Module 3 Part 2
- Monitoring:
	- Cloudwatch: our central nervous system for monitoring. It gathers vital **metrics, logs, and events** from across our AWS environment, allowing us to visualize performance on **dashboards**, set up **alarms** for immediate notification, and even trigger **automated actions** to resolve problems.
- Security:
	- Security groups: instance level firewall
	- Network Access Control List: subnet level firewall
	- AWS Shield: primarily for DDOS attacks. 
	- Web Application Firewall: for common web vulnerabilities such as SQL injection, cross site scripting, etc. Can rate limit.
	- Network Firewall: operates like a standard firewall. control traffic based on security policies. Data Loss Prevention. Deep packet inspection: look at the contents of the packet and match it to signatures to block suspicious packets.
- Scaling:
	- Load balancers: load balances to the EC2 instances
	- auto scaling groups: automatically scales EC2 instances based on traffic
	- Aurora serverless: automatically scales up server performance based on usage.
	- dynamo DB: performance at scale, no SQL database, managed. No complex SQL queries. Very fast and infinitely scalable. Requires well defined access patterns: user account number -> user account info, real time leaderboards 
	- Elasticache: cache for the database.
- Object based storage
	- S3 Bucket: every object has metadata (file name, size, permissions, tags, etc) and the data itself (video, backup files, word files).
- AWS tool to improve security, costs, monitor service limits
	- AWS Trusted Advisor: inspects the your AWS environment to provide guidance based on best practices. Part of Business Support Plan
		- Cost optimization: identify idle or underutilized resources. Offers recommendations to reduce costs.
		- Performance: check for resource configurations, maybe EC2 with very high CPU usage.
		- Security: identifies potential security weaknesses, weak security group rules, publicly accessible S3, enabling MFA
		- Service limits: monitors our the usage of AWS services against our quotas.
	- AWS Cost explorer and AWS Budgets
		- Cost visualization and analysis.
		- Create budgets for AWS costs. Notifies if budget threshold is met. Automatic action when threshold is met.






- Route 53: health checks on our servers to not send traffic to black hole. Geographically diverse DNS servers. Weighted routing: distribute traffic to many of our servers. Latency based routing: routes the user to the server with the lowest latency for that user. 
- Monitoring:
	- Cloudwatch: our central nervous system for monitoring. It gathers vital **metrics, logs, and events** from across our AWS environment, allowing us to visualize performance on **dashboards**, set up **alarms** for immediate notification, and even trigger **automated actions** to resolve problems.
- Security:
	- Security groups: instance level firewall
	- Network Access Control List: subnet level firewall
	- AWS Shield: primarily for DDOS attacks. 
	- Web Application Firewall: for common web vulnerabilities such as SQL injection, cross site scripting, etc. Can rate limit.
	- Network Firewall: operates like a standard firewall. control traffic based on security policies.
- AWS tool to improve security, costs, monitor service limits
	- AWS Trusted Advisor: inspects the your AWS environment to provide guidance based on best practices. Part of Business Support Plan
		- Cost optimization: identify idle or underutilized resources. Offers recommendations to reduce costs.
		- Performance: check for resource configurations, maybe EC2 with very high CPU usage.
		- Security: identifies potential security weaknesses, weak security group rules, publicly accessible S3, enabling MFA
		- Service limits: monitors our the usage of AWS services against our quotas.
	- AWS Cost explorer and AWS Budgets
		- Cost visualization and analysis.
		- Create budgets for AWS costs. Notifies if budget threshold is met. Automatic action when threshold is met.
- Automation: 
	- CloudFormation: automates provisioning of infrastructure (EC2, databases, S3, VPCs) in an automated and repeated way. 
		- You essentially create JSON files with an AWS infrastructure, define all of the parameters of the infrastructure, set the condition for when this infrastructure is created.
	- Auto scaling group for EC2
	- serverless aspect of the Aurora Databases
- Object based storage
	- S3 Bucket: every object has metadata (file name, size, permissions, tags, etc) and the data itself (video, backup files, word files).
- Scaling:
	- Load balancers: load balances to the EC2 instances
	- auto scaling groups: automatically scales EC2 instances based on traffic
	- Aurora serverless: automatically scales up server performance based on usage.
	- dynamo DB: performance at scale, no SQL database, managed. No complex SQL queries. Very fast and infinitely scalable. Requires well defined access patterns: user account number -> user account info, real time leaderboards 
	- Elasticache: cache for the database.

# Database
- Using Relational Database Server (RDS) - managed database service, AWS handles the the nitty gritty details, you work with the database.
- Install the dependencies, the database itself, the authentications and permissions, configure the firewall.
- Authentication: using IAM that integrates with AD
- Endpoint: the domain name that you use to reach the database



- how much charged to move 30 gb out of database, how much charged to move 5gb into
- what is IOPS, storage for databases

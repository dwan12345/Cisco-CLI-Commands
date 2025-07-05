1. To ensure HA and scalabilty, I implemented a multi Availability Zone architecture within a VPC. The public subnets will contain the web servers and load balancers. The private subnets will control the database.
2. An application load balancer will be used to ensure high availability and to provide scalability. The load balancer will easily be able to handle up to 100 requests a second. It also provides automatic health checks on our EC2 instances.
3. To adjust to demand while keeping costs low, we will use EC2 Auto Scaling. It will keep track of statistics such as CPU utilization and requests per target to automatically scale up or down the amount of EC2 instances we have.
4. The instance type we will be using for the webserver is T4g.small, which provides 2 vCPUs and 2 Gb of RAM. This is a good starting point as this is well above the minimum requirements set forth. If in the future, the CPU utilization is consistently high, then we can always use a more powerful instance type. 
5. For our databases, we will be using Amazon Relational Database Server (RDS). The engine choice is up to Sea Ice Creamery. The instance type will be db.m7g.large, which provides 2 vCPUs and 8 gb of RAM. 
6. Crucial for HA, RDS maintains a backup replica in another AZ, which will ensure business operation in case of a outage. Data replication is also free.
7. The storage we will use is gp3 for balanced price and performance. The capacity 50 gb. We can always upgrade later if needed.
8. For domain name registration, we will be using Route 53. This has global coverage along with HA.
9. Business Support because enterprise support is overkill. It provides access to fast response times and AWS support engineers.


# Database
- Using Relational Database Server (RDS) - managed database service, AWS handles the the nitty gritty details, you work with the database.
- Install the dependencies, the database itself, the authentications and permissions, configure the firewall.
- Authentication: using IAM that integrates with AD
- Endpoint: the domain name that you use to reach the database



- how much charged to move 30 gb out of database, how much charged to move 5gb into
- what is IOPS, storage for databases

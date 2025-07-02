# Infoblox Project
I had significant experience configuring and managing core network services including DHCP, DNS, Active Directory, and NTP. We utilized a hybrid environment, leveraging both **Infoblox appliances** and **Microsoft Windows Servers** for these critical functions.

**Specifically regarding Infoblox, we had a redundant pair setup,** which was crucial for maintaining high availability. I was responsible for the initial configuration, ensuring the two appliances were properly synchronized and that failover mechanisms were thoroughly tested. This involved configuring DHCP scopes and NTP settings along with integrating them with our Active Directory environment to centralize access control.

On the **Microsoft side**, I regularly managed DNS records, and Active Directory objects, including user accounts, and group policies. I also configured and maintained NTP services on our domain controllers, ensuring accurate time synchronization across the network, which is vital for Kerberos authentication and overall system integrity.

# SIC
I have direct experience designing highly redundant networks for critical environments, most notably for a client's corporate headquarters

My approach always begins with understanding the client's **tolerance for downtime and their specific traffic profiles**. For this HQ project, the client required near 100% uptime, which dictated a **full meshed redundancy strategy** at the core and distribution layers, including redundant switching hardware, dual power supplies, and diverse fiber paths. 

Throughout the design phase, I'm always reviewing the **bill of materials to stay within budget**, often presenting trade-offs between different vendor solutions and performance tiers to the client. I worked closely with their IT team to ensure the proposed design would **integrate smoothly with their existing IP schema, security appliances, and application servers**, preventing any compatibility issues. 

For example, their finance department required specific parameters to ensure security. I designed a dedicated network segment (VLAN) for their systems and implemented specific routing policies on our core network devices. This ensured that all traffic originating from that VLAN was forced through their finance proxy server, which allowed us to configure more granular security policies.


# AWS

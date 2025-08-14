
### Interview Questions & Answers for Sanofi Connectivity Services Team / STORM Project

**Category 1: Understanding of the Role & Team**

**1. Question:** Based on the provided scope, how do you see your role contributing to the success of the Sanofi Connectivity Services team and specifically the STORM project?

**Answer:** "My understanding is that the Connectivity Services team is critical for maintaining robust and secure network infrastructure across Sanofi's 200 sites, covering everything from lifecycle management to security and support. The STORM project specifically addresses network obsolescence and modernization in the AMER region. My contribution would primarily involve actively participating in the full lifecycle of network hardware refreshes, from understanding existing topologies and designing new environments, to meticulous planning, installation, and migration. My focus would be on ensuring minimal business impact during migrations, providing comprehensive documentation, and facilitating a smooth handover to the operational team. By effectively managing these technical and logistical aspects, I would help the team achieve faster deployments, increase scalability, and free up internal engineers to focus on future network architecture."

**2. Question:** The document emphasizes that "communication, due diligence, and detailed planning are critical to the success of these projects." Can you elaborate on how you would ensure these three aspects are consistently met in your work?

**Answer:** "Firstly, **communication** would be paramount. This involves regular, clear, and proactive communication with local site contacts, internal Sanofi teams, and the business stakeholders. I would establish communication plans, provide timely updates on project progress, potential issues, and upcoming changes. For example, during migration planning, I'd ensure business users are well-informed about maintenance windows and expected impacts.

**Due diligence** means a thorough investigation and understanding of the current state before any changes are made. This includes detailed network topology reviews, understanding existing configurations, identifying dependencies, and assessing potential risks. It also means thoroughly vetting new hardware specifications and ensuring they align with Sanofi's standards and future needs.

**Detailed planning** would involve creating comprehensive project plans, including step-by-step migration procedures, rollback plans, contingency plans, and testing protocols. I'd ensure all stakeholders agree on the plan, and that every aspect, from rack space and power requirements to cabling and IP addressing, is accounted for before any physical work begins. This meticulous approach minimizes surprises and ensures a smooth execution."

---

**Category 2: Technical Knowledge (Networking & Security Hardware)**

**3. Question:** Sanofi uses Cisco ( Nexus/IOS ) switches and routers, Aruba wireless, and Palo Alto firewalls/SD-WAN. Describe your experience with these specific vendors and technologies, particularly concerning network lifecycle management.

**Answer:** "I have extensive hands-on experience with Cisco IOS for routers and switches, including configuration of routing protocols (OSPF, BGP), VLANs, STP, HSRP/VRRP, and QoS. My experience extends to Cisco Nexus platforms for data center environments, understanding their architecture and high-density capabilities. With Aruba wireless, I've worked on deploying and managing controllers and access points, focusing on secure SSID configuration, guest access, and performance optimization.

My security experience heavily involves Palo Alto Networks. I've deployed and managed Palo Alto Firewalls, configuring security policies, NAT, VPNs (IPSec/SSL-VPN), and leveraging features like App-ID and User-ID. For network lifecycle, I've been involved in planning hardware refresh cycles, performing like-for-like replacements, and sometimes designing upgrades to newer platforms within these vendor ecosystems. This includes migrating configurations, validating new hardware performance, and ensuring seamless integration into the existing network."

**4. Question:** Sanofi is currently using Palo Alto SD-WAN. Can you explain the core benefits of SD-WAN over traditional WAN architectures and what considerations are important when implementing or migrating to an SD-WAN solution like Palo Alto's Prisma SD-WAN?

**Answer:** "The core benefits of SD-WAN, especially solutions like Palo Alto's Prisma SD-WAN, over traditional WANs are significant. Firstly, **cost optimization** by leveraging commodity internet links (broadband, LTE) instead of expensive MPLS circuits. Secondly, **improved application performance and user experience** through intelligent path selection based on real-time link quality, ensuring critical applications get optimal bandwidth and low latency. Thirdly, **operational simplicity and agility** due to centralized management, automation, and zero-touch provisioning, which simplifies branch deployments and management. Lastly, **enhanced security** through integrated security services, which is a key differentiator for Palo Alto's offering, allowing for a secure direct-to-internet access.

When implementing or migrating, key considerations include:

- **Application identification and prioritization:** Clearly defining which applications are critical and how their traffic should be handled.
    
- **Security integration:** Ensuring the SD-WAN solution seamlessly integrates with existing security policies and infrastructure, especially with Palo Alto's security stack.
    
- **Underlay network readiness:** Confirming the underlying internet and MPLS links are robust enough.
    
- **Migration strategy:** Developing a phased migration plan to minimize business disruption.
    
- **Monitoring and visibility:** Establishing robust monitoring tools to track performance and troubleshoot issues in the new SD-WAN environment.
    
- **Training:** Ensuring operational teams are trained on the new SD-WAN platform."
    

---

**Category 3: Project Management & Lifecycle**

**5. Question:** The STORM project involves refreshing network hardware every 5 years. Describe a typical network hardware refresh project you've managed or been a significant part of, highlighting the phases and your specific responsibilities.

**Answer:** "A typical network hardware refresh project I've been involved in follows several phases. It usually starts with an **Assessment Phase**, where we audit the existing hardware, identify end-of-life dates, and analyze current network performance and capacity. My role here involves collecting data, reviewing network diagrams, and understanding the business requirements at specific sites.

Next is the **Design Phase**. This involves selecting new hardware (e.g., specific Cisco Nexus models, Aruba APs), designing the new topology, creating IP addressing schemes, and planning for integration with existing systems (monitoring, authentication). I'd contribute by proposing suitable architectures, creating detailed design documents, and getting stakeholder approval.

The **Procurement Phase** involves scoping, quoting, and ordering the new equipment, ensuring lead times align with project schedules. My responsibility would be to accurately determine hardware requirements and work with vendors.

Then comes **Implementation and Migration**. This is the most critical phase. It involves preparing the new hardware (racking, cabling), pre-configuring devices, and most importantly, developing a detailed migration plan. This plan includes pre-checks, step-by-step cutover procedures (often during off-hours), rollback plans, and post-migration validation. I would lead or significantly contribute to executing the cutover, minimizing downtime, and immediately troubleshooting any issues.

Finally, the **Post-Implementation Phase** includes updating all documentation (CMDB, network diagrams), integrating new devices into monitoring systems, and performing a thorough handover to the operational team with necessary training. My role here is to ensure all documentation is accurate and complete, and that the operations team is ready to support the new environment."

**6. Question:** "Migration planning from old hardware to new hardware with minimal impact to the business" is a key task. What strategies or techniques do you employ to achieve minimal business disruption during network migrations?

**Answer:** "Achieving minimal business disruption during network migrations requires meticulous planning and a multi-faceted approach. My strategies typically include:

1. **Thorough Pre-Migration Analysis:** Deep dive into the current network topology, application dependencies, and traffic flows to identify all potential impact points.
    
2. **Detailed Migration Plan:** Develop a step-by-step plan that includes pre-checks, the exact sequence of configurations, cutover procedures, verification steps, and a clear rollback plan. This plan is shared and reviewed with all stakeholders.
    
3. **Staging and Pre-configuration:** Wherever possible, new hardware is pre-configured and staged off-site or in a lab environment to minimize on-site work and reduce errors.
    
4. **Phased Rollouts:** Instead of a big-bang approach, I prefer phased migrations (e.g., migrating by VLAN, by department, or by device stack) to isolate potential issues and limit the blast radius.
    
5. **Change Windows:** Schedule migrations during low-impact business hours, such as nights or weekends, after clear communication and agreement with the business.
    
6. **Redundancy Leverage:** Utilize existing network redundancies (e.g., redundant links, HSRP/VRRP, ECMP) to perform migrations on one path while the other maintains connectivity, then switch traffic.
    
7. **Automated Validation/Testing:** Use scripts or automated tools for pre- and post-migration validation (e.g., ping tests, traceroutes, checking BGP/OSPF adjacencies, verifying critical application connectivity) to quickly confirm success.
    
8. **Constant Communication:** Maintain open communication channels with the business during the migration window, providing real-time updates and quick responses to any reported issues.
    
9. **Clear Rollback Plan:** Always have a well-tested rollback plan ready, allowing a swift return to the previous state if unforeseen critical issues arise.
    
10. **Experienced Team:** Ensure the migration team is well-versed with the plan and has the necessary expertise to troubleshoot on the fly."
    

---

**Category 4: Troubleshooting & Problem Solving**

**7. Question:** Describe your methodology for troubleshooting a complex network issue, perhaps one that involves multiple network layers or technologies mentioned (e.g., a performance issue spanning wireless, switches, and a firewall).

**Answer:** "My troubleshooting methodology is systematic, often following a layered approach like the OSI model, but I'll adapt based on the problem.

1. **Gather Information:** First, I'd gather as much information as possible: user reports (what's the symptom?), recent changes, error messages, and baseline performance data.
    
2. **Define the Scope:** Is it affecting one user, a department, a specific application, or an entire site? This helps narrow down the problem domain.
    
3. **Verify Basics:** Start with the simplest checks: physical connectivity (cabling, links up/down), IP addressing, DNS resolution.
    
4. **Layer-by-Layer Approach:**
    
    - **Layer 1 (Physical):** Check cables, SFP modules, port status.
        
    - **Layer 2 (Data Link):** Look at MAC address tables, VLANs, STP status on switches. For wireless, check client associations, signal strength.
        
    - **Layer 3 (Network):** Verify IP routing tables, ARP entries, connectivity tests (ping, traceroute) to determine reachability.
        
    - **Layer 4 (Transport):** Check firewall rules for port blocking, verify TCP/UDP sessions.
        
    - **Layer 7 (Application):** If network layers appear fine, investigate application-specific issues, server-side problems, or misconfigurations.
        
5. **Tools & Logs:** Utilize tools like show commands on Cisco/Aruba devices, logs on Palo Alto Firewalls, network monitoring tools (NMS), packet captures (Wireshark), and performance monitors to pinpoint bottlenecks or errors.
    
6. **Isolate & Test:** Once a potential cause is identified, I'd try to isolate it and test a hypothesis. This might involve disabling a feature, bypassing a device (if safe), or making a small configuration change.
    
7. **Document & Resolve:** Document the problem, the steps taken, the resolution, and any lessons learned. This is crucial for future reference and knowledge sharing."
    

---

**Category 5: Soft Skills & Collaboration**

**8. Question:** The role requires "Collaboration with other teams within Digital." Can you give an example of a time you successfully collaborated with another IT team (e.g., server, application, or security team) to resolve a complex issue or deliver a project?

**Answer:** "Certainly. In a previous role, we were experiencing intermittent performance issues with a critical manufacturing application. Initially, it was suspected to be a network problem. I collaborated closely with the application team and the server team.

My team focused on network monitoring, verifying latency, packet loss, and bandwidth utilization across the network path from the user to the application servers, and through the firewall. The server team analyzed server resource utilization, while the application team looked at application logs and database performance.

Through regular sync-up meetings, sharing data points from our respective monitoring tools, and joint troubleshooting sessions, we discovered the network was performing within expected parameters. The root cause was eventually traced to a specific database query taking an unusually long time, which was impacting the application's response. Our collaboration allowed us to systematically rule out the network, provide data to the other teams, and ultimately help them pinpoint the issue. This cross-functional effort ensured the problem was resolved efficiently without finger-pointing and built stronger relationships between the teams."

---

**Category 6: Local Onsite Support & Travel**

**9. Question:** The position requires local onsite support, and at least one resource should be within commuting distance of the Washington, DC area. How do you feel about traveling to various Sanofi sites (approximately 13 sites year over year) and providing hands-on support?

**Answer:** "I understand that local onsite support and travel to approximately 13 sites per year in the AMER region is a fundamental requirement for this role, especially given the hands-on nature of hardware installations and migrations. I am comfortable with business travel and providing direct onsite support. I recognize the critical need for a physical presence for tasks like rack and stack, cabling, and initial device configuration, which cannot be done remotely. Being within commuting distance of the Washington, DC area makes me an ideal candidate for providing rapid response when needed. I see this as an essential part of ensuring successful project delivery and supporting Sanofi's critical business functions at their manufacturing locations."



### ????
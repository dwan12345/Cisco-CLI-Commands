# Traffic Flow
1. Client attempts to resolve example.com
2. client goes to their local DNS server
3. their local DNS server goes to root DNS server
4. root DNS goes to TLD server (the .com server)
5. the TLD has the NS records that point to the authoritative DNS for example.com
6. the TLD forwards the DNS request to the authoritative server
7. the authoritative server responds back, bouncing along the chain of communication to reach the client

# Records
- A - domain name to IPv4
- AAAA - domain name to IPv6
- CNAME - domain name to another domain name
- NS (Nameserver) - maps the domain name to the IP of the authoritative DNS of that domain 

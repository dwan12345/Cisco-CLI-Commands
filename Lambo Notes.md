# Doing Stuff No Downtime
- using DNS to perform cutovers
- using HA clustering to minimize downtime
- using features of the hardware itself, such as double route processors, to minimize downtime


# Lambo Questions
- are documentation up to date? ask your peers at the company
- should I spend time learning automation? yes, if you have time. but companies will use wildly different ways to do automation
- in wireless, how do you account for super high density places? places with more people, add more access points
- is packet size of the applications being used relevant in planning a modern wireless environment? not that important
- first weeks of contract - asking for documentation. asking for meetings to be sitting in and shadowing. figure out their workflow process, how they communicate, how they do meetings. once you get your access, figure out your first deliverables. 
- what should I avoid doing while on contract - don't be quiet, don't be afraid to say stupid stuff, talk to people, offer ideas. do not look like you are just trying to do the minimum. ask why they did the network this way. when you make a mistake, talk to the escalation team.
- when you get a new project: write down all questions, walk away for an hour, write down all new questions, then email it.
- what are the characteristics of MPLS circuits? why do we still use them when we have SD-WAN? Are they more secure than regular circuits? can you access the internet through them? you cannot access the internet with only the MPLS, but you can use MPLS back to a data center which has a connection to the internet. MPLS has more options for SLAs for uptime, which regular internet connections do not. Internet will never honor QOS markings, but MPLS does honor QOS. companies are entrenched in MPLS, so it makes it hard to switch to SD-WAN
- is QOS relevant today? not really relevant too much today because we have so much bandwidth. we have skype forever now
- how do you know which security policies to deploy? use APP-ID to explicitly allow the needed traffic. use a detailed naming convention
- there are device hardening guides from every vendor.
- you should do security updates at least once every 2 weeks. perform a risk assessment such that is you get compromised, you estimate how much money they lose. this helps executives allocate money for security.
- palo alto decryption: PA create its own self sign certificate. cisco ISE can require your device to trust the PA certificate, or the device needs to be configured to trust the certificate. this is forward proxy
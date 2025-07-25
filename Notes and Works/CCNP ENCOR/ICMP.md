- within protocol field of IP headers, ICMP packets have a value of 1
- ICMP is not a layer 4 protocol, it is considered part of the IP protocol

# ICMP Message Types
- destination unreachable: type 3. self explanatory. the code field says why it was unreachable
- redirect: type 5.  inform hosts to use a different router to reach the destination. code field says what type of redirect
- time exceeded: type 11. to inform the sender that the TTL expired, or to inform the sender that not all fragments of the packet arrived in time so it had to discard it. code field says which of the 2 scenarios happened
- echo request: type 8. Like a regular ping. code field of 0
- echo reply: type 0. a reply to a regular ping. code field of 0

# ICMPv6
- ICMP but for IPv6
- pretty much the same as ICMPv4, but the types are different.
- NDP uses ICMPv6, there are specific types of ICMPv6 used specifically for NDP
- does not have the message "fragmentation needed, but DF bit set" because IPv6 does not fragment packets


# Commands
- do not reply to ICMP messages with unreachable messages
```js
conf t
int <interface>
no ip unreachables
end
```
- disable ICMP redirects
```js
conf t
int <interface>
no ip redirects
end
```








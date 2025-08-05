- scripting language that allows you to intercept and modify the traffic beyond the standard capabilities of the LTM
- there are some use cases that can be done using local traffic policies. local traffic policies should be preferred over iRules because they perform better, easier to manage
- common use cases:
	- custom content switching: directing traffic to different pools based on URI, HTTP headers, cookies, source IP, etc.
	- modify HTTP header, server responses
	- block specific clients based on geolocation
	- directing traffic based user's device: a specific pool used to serve mobile clients
	- A/B testing, sending some users to a newer application for testing
- Best practices:
	- keep them simple. iRules can be CPU intensive and be troublesome to troubleshoot
	- use built in features first
	- use "return" or "event disable" commands to stop further processing of an iRule once the condition has been met
	- test in lab environment to make sure there are no side effects or performance impacts
- create iRules:
	- local traffic -> iRules -> iRules list -> create

# Syntax
- the format of iRules:
```js
when <event> {
	if {<conditional>} {
		<action>
	}
}
```
- example events
	- CLIENT_ACCEPTED: when TCP 3 way handshake is done
	- CLIENT_CLOSED: when a client side TCP is closed
	- HTTP_REQUEST: when F5 gets the complete HTTP header from client
	- HTTP_RESPONSE: when F5 gets response back from server
	- CLIENTSSL_HANDSHAKE: after a successful SSL handshake


- apply iRule: 
	- local traffic -> virtual server -> virtual server list -> *click on VS* -> resources -> *manage iRules*
	- 
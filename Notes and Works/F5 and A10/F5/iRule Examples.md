```js
when CLIENT_ACCEPTED {
    if { [IP::addr [IP::client_addr] equals 10.10.10.10] } {
        pool my_pool
    }
 }
```
- IP::addr - says the next object is an IP address
- IP::client_addr - grabs the client address
- pool my_pool - send this traffic to a pool called my_pool


```js
when HTTP_REQUEST {
    if { [HTTP::uri] ends_with ".gif" } {
        if { [LB::status pool my_Pool member 10.1.2.200 80] eq "down" } {
            log "Server $ip $port down!"
            pool fallback_Pool
        } else {
            pool my_Pool member 10.1.2.200 80
        }
    }
}
```
- \[HTTP::uri] - grabs the URI of the http request
- LB::status - check on the status of an object
- pool my_Pool member 10.1.2.200 80 - references a specific member within a pool at a port

```js
when HTTP_REQUEST {
    if { [HTTP::uri] ends_with ".gif" } {
        node 10.1.2.200 80
    }
}
```
- node 10.1.2.200 80 - send to a specific node at port 80. 

```js
when HTTP_REQUEST {
    virtual my_post_processing_server
}
when HTTP_REQUEST {
    log local0. "Current virtual server name: [virtual name]"
}
```
- both blocks run when the F5 receives the full http header
- virtual my_post_processing_server - send the traffic to another VS called my_post_processing_server
	- use case: first F5 handles SSL offloading, security, and second F5 handles load balancing. this way, the iRules and policies are separate and easier to debug
- log local0. - logs to /var/log/ltm. this is standard practice
- \[virtual name] - grabs the name of the current VS

```js
when HTTP_REQUEST {
    if { [HTTP::uri] eq "/app1?user=admin" } {
        HTTP::redirect "http://www.example.com/admin"
    }
}
```
- HTTP::redirect - sends a 302 redirect to the client to another URL
```js
when CLIENT_ACCEPTED {
    if { [TCP::local_port] != 443 } {
        reject
    }
}
```
- TCP::local_port - the port on the VS that the client connects to
- reject - terminates the connection


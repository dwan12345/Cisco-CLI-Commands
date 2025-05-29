- ports can be automatically disabled based on certain conditions such as port security configs, or DHCP snooping rate limiting.
- can configure automatic recovery from error disabled

## Error Disable Recovery
- port security cause: psecure-violation
- DHCP snooping rate limit: dhcp-rate-limit
```js
! enable error disable on port security
conf t
errdisable recovery cause [some cause]
! errdisable recovery interval [seconds]
end
```


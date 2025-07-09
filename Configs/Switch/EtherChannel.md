## LACP
- Link Aggregation Control Protocol
- Open standard, and the industry standard
```js
! configures LACP on some interfaces
conf t
int range <interface range>
channel-group <number> mode active
end
```

## PAgP
- cisco proprietary Port Aggregation Protocol
```js
! configures PAgP on some interfaces
conf t
int range <interface range>
channel-group <number> mode desirable
end
```


## Regular Etherchannel
```js
! configures regular etherchannel on some interfaces
conf t
int range <interface range>
channel-group <number> mode on
end
```

## Show Commands
```js
show etherchannel summary
show etherchannel port-channel
```










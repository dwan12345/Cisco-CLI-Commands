- accurate time is for accurate logs for troubleshooting
- a


## Get Info From Another NTP Server
- Can specify multiple in case one goes down. The router will use the most reliable server
```js
! get time info from a ntp server
conf t
ntp server <ntp server ip>
ntp server <ntp server ip>
end
```

## Configure an NTP server
- Make sure the router is getting NTP info from somewhere
- the interface should be a loopback interface
```js
! configure NTP server
cont f
ntp source <interface>
end
```

## Manually Set the Time
- clock set is software clock
- calendar set is hardware clock
```js
! manually set the clock time
clock set <hh:mm:ss> <day of month> <month> <year>
calendar set <hh:mm:ss> <day of month> <month> <year>
```

## Update the Software Clock to/from Hardware Clock
- clock update-calendar: update hardware clock from software clock
- clock read-calendar: update software clock from hardware clock
```js
clock update-calendar
clock read-calendar
```

## Sync Hardware Clock with NTP
```js
!
conf t
ntp update-calendar
end
```


## Show
```js
show clock
show clock detail
show ntp associations
show ntp status
```

## Dynamic Trunking Protocol
- Cisco proprietary
- dynamically allow interface to become trunk or access port
- enabled by default

## DTP Configs
- Trunk port and desirable port will actively send out DTP frames to form trunk. Auto mode does not, but it will accept the DTP frames. Access mode does not accept the frames.
```js
! set the DTP mode
conf t 
switchport mode dynamic <auto | desirable>
end
```
- turn off DTP. setting mode to access will automatically turn off DTP.
```js
! turn off DTP
conf t
switchport nonegotiate
end
```
- Show
```js
show int <interface> switchport
```


## VLAN Trunking Protocol
- Cisco proprietary 
- Configure a VTP server switch, other switches will synchronize VLAN database to the server.
- VTP modes: cisco switches are default to server
	- Server: can add, modify, and delete vlans. Everytime a change is made, the "revision number" is incremented. The highest revision number will take priority. Also function as VTP clients, where the server will sync to the higher revision number server
	- clients: cannot add, modify, or delete vlan. will sync to highest revision number. will advertise and forward VTP database
	- transparent: do not sync vlan database, they do not advertise their own vlans, but will forward VTP frames

## VTP Configs
- Set VTP domain
```js
! set VTP domain
conf t
vtp domain <domain name>
end
```
- Set VTP mode
```js 
! set VTP mode
conf t
vtp mode <server | client | transparent>
end
```
- change VTP version
```js
! change vtp version
conf t
vtp version <1 | 2 | 3>
end
```
- Show
```js
show vtp status
```






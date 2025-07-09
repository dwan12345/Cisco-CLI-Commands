# Set Up DNS
```js
! set up router as DNS
conf t
ip dns server
ip host <host name> <ip>
ip name-server <ip of external DNS>
end
```
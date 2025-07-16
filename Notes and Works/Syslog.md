# Message Format
[seq] : [time stamp] : %[facility] - [severity] - [mnemonic] : [description]
- seq: sequence number, indicates order of messages
- time stamp: the time stamp
- facility: what process generated the message, such as OSPF
- severity: the severity
- mnemonic: short code for the message indicating what happened
- description: the description
- The seq and time stamp may not be displayed based on configuration

# Severity Levels
- Emergencies Are Critical Even When Nobody Is Dead
0. Emergency
1. Alert
2. Critical
3. Error
4. Warning
5. Notice
6. Informational
7. Debugging


- Logging console 5 will not show level 6 and 7 severity levels
```js
conf t
logging console <0-7>
end
```
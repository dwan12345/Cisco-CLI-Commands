
ip sla 1
icmp-echo 8.8.8.8
timeout 2000
threshold 500
frequency 5
exit
ip sla schedule 1 start-time now life forever

track 1 ip sla 1 reachability

ip route 0.0.0.0 0.0.0.0 ?? track 1
ip route 0.0.0.0 0.0.0.0 ?? 50
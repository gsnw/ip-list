# ip-list
IP-Address List for ACL rules

# HowTo use

## OpenBSD/FreeBSD/NetBSD PF (Packet Filter)

Example allow ssh over /etc/pf.conf
```
table <telekom> persist file "/etc/ip-list/isp/telekom-ipv4"
# Allow only IP-Adress from telekom to access SSH Port 22
pass in log on $ext_if inet proto tcp from <telekom> to $ext_if port 22 keep state
```

## Linux (IPTables)

Example allow ssh over bash script
```
while read ipaddr
do
	iptables -A INPUT -p tcp -s $ipaddr --dport 22 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
done < /etc/ip-list/isp/telekom-ipv4 | sort | uniq
iptables -A OUTPUT -p tcp --sport 22 -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

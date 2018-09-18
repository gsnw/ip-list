# ip-list
IP-Address List for ACL rules

# HowTo use

## OpenBSD/FreeBSD/NetBSD PF (Packet Filter)

```
table <telekom> persist file "/etc/ip-list/telekom-ipv4"
# Allow only IP-Adress from telekom to access SSH Port 22
pass in log on $ext_if inet proto tcp from <telekom> to $ext_if port 22 keep state
```

## Linux (IPTables)

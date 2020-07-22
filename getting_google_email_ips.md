```C:\Windows\System32>nslookup -q=TXT _netblocks.google.com
Server:  commandsoc.domain.local
Address:  192.168.2.15

Non-authoritative answer:
_netblocks.google.com   text =

        "v=spf1 ip4:35.190.247.0/24 ip4:64.233.160.0/19 ip4:66.102.0.0/20 ip4:66.249.80.0/20 ip4:72.14.192.0/18 ip4:74.125.0.0/16 ip4:108.177.8.0/21 ip4:173.194.0.0/16 ip4:209.85.128.0/17 ip4:216.58.192.0/19 ip4:216.239.32.0/19 ~all"

C:\Windows\System32>nslookup -q=TXT _netblocks2.google.com
Server:  commandsoc.domain.local
Address:  192.168.2.15

Non-authoritative answer:
_netblocks2.google.com  text =

        "v=spf1 ip6:2001:4860:4000::/36 ip6:2404:6800:4000::/36 ip6:2607:f8b0:4000::/36 ip6:2800:3f0:4000::/36 ip6:2a00:1450:4000::/36 ip6:2c0f:fb50:4000::/36 ~all"

C:\Windows\System32>nslookup -q=TXT _netblocks3.google.com
Server:  commandsoc.domain.local
Address:  192.168.2.15

Non-authoritative answer:
_netblocks3.google.com  text =

        "v=spf1 ip4:172.217.0.0/19 ip4:172.217.32.0/20 ip4:172.217.128.0/19 ip4:172.217.160.0/20 ip4:172.217.192.0/19 ip4:172.253.56.0/21 ip4:172.253.112.0/20 ip4:108.177.96.0/19 ip4:35.191.0.0/16 ip4:130.211.0.0/22 ~all"
```

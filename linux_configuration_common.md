## Static IP set
- vim /etc/sysconfig/network-scripts/ifcfg-ens192
```	BOOTPROTO="none"
	PREFIX=24
	IPADDR=10.1.2.X
	NETMASK=255.255.255.0
	GATEWAY=192.168.2.254
	DNS1=192.168.2.15```
- systemctl restart network

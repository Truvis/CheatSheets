# Remove connection floods to log file

## CentOS 7
- /usr/lib/systemd/system/snmpd.service
- Environment=OPTIONS="-LS0-4d"
- systemctl daemon-reload
- systemctl restart snmpd

## CentOS 6
- /etc/sysconfig/snmpd
- OPTIONS='-Lsd -Lf /dev/null'

## ESXi 5.x
- vicfg-snmp.pl --server hostname --username your_username --password your_password -c YOUR_STRING
- vicfg-snmp.pl --server hostname --username your_username --password your_password -p 161
- vicfg-snmp.pl --server hostname --username your_username --password your_password --enable

## ESXi 5.5
- esxcli system snmp set --communities YOUR_STRING
- esxcli system snmp set --enable true
- esxcli network firewall ruleset set --ruleset-id snmp --allowed-all true
- esxcli network firewall ruleset set --ruleset-id snmp --enabled true
- /etc/init.d/snmpd restart

## ESXi 6.x
- esxcli system snmp set -r
- esxcli system snmp set -c YOUR_STRING
- esxcli system snmp set -p 161
- esxcli system snmp set -L "City, State, Country"
- esxcli system snmp set -C noc@example.com
- esxcli system snmp set -e yes


REFS:
- https://serverfault.com/questions/727084/how-to-clear-or-stop-net-snmpd-log
- https://serverfault.com/questions/310640/reduce-snmpd-logging-verbosity
- https://support.auvik.com/hc/en-us/articles/206311526-How-to-enable-SNMP-on-a-VMware-ESXi-hypervisor

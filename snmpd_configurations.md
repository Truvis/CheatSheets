# Remove connection floods to log file

## CentOS 7
- /usr/lib/systemd/system/snmpd.service
- Environment=OPTIONS="-LS0-4d"
- systemctl daemon-reload
- systemctl restart snmpd

## CentOS 6
- /etc/sysconfig/snmpd
- OPTIONS='-Lsd -Lf /dev/null'


REFS:
- https://serverfault.com/questions/727084/how-to-clear-or-stop-net-snmpd-log
- https://serverfault.com/questions/310640/reduce-snmpd-logging-verbosity

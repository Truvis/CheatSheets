# Remove connection floods to log file
## CentOS 7
- /etc/sysconfig/snmpd
- OPTIONS='-Lsd -Lf /dev/null'


REFS:
- https://serverfault.com/questions/727084/how-to-clear-or-stop-net-snmpd-log
- https://serverfault.com/questions/310640/reduce-snmpd-logging-verbosity

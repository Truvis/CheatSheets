# Remove connection floods to log file
## CentOS 7
- /etc/sysconfig/snmpd
- OPTIONS='-Lsd -Lf /dev/null'

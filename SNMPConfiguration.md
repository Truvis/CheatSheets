# SNMP Setup for sending information

## CentOS
curl -o /usr/local/bin/distro https://gitlab.com/observium/distroscript/raw/master/distro
chmod +x /usr/local/bin/distro

snmpd.conf:
extend .1.3.6.1.4.1.2021.7890.1 distro /usr/local/bin/distro

extend .1.3.6.1.4.1.2021.7890.2 hardware /bin/cat /sys/devices/virtual/dmi/id/product_name

extend .1.3.6.1.4.1.2021.7890.3 vendor   /bin/cat /sys/devices/virtual/dmi/id/sys_vendor

extend .1.3.6.1.4.1.2021.7890.4 serial   /bin/cat /sys/devices/virtual/dmi/id/product_serial

extend uptime /bin/cat /proc/uptime

In some environments snmpd not have permission for read file /sys/devices/virtual/dmi/id/product_serial. Need to change file permission at boot by adding this command to /etc/rc.local: chmod 444 /sys/devices/virtual/dmi/id/product_serial

## Debian
curl -o /usr/local/bin/distro https://gitlab.com/observium/distroscript/raw/master/distro
chmod +x /usr/local/bin/distro

snmpd.conf:
extend .1.3.6.1.4.1.2021.7890.1 distro /usr/local/bin/distro
extend .1.3.6.1.4.1.2021.7890.2 hardware /bin/cat /sys/devices/virtual/dmi/id/product_name
extend .1.3.6.1.4.1.2021.7890.3 vendor   /bin/cat /sys/devices/virtual/dmi/id/sys_vendor
extend .1.3.6.1.4.1.2021.7890.4 serial   /bin/cat /sys/devices/virtual/dmi/id/product_serial
extend uptime /bin/cat /proc/uptime

In some environments snmpd not have permission for read file /sys/devices/virtual/dmi/id/product_serial. Need to change file permission at boot by adding this command to /etc/rc.local: chmod 444 /sys/devices/virtual/dmi/id/product_serial

## Windows

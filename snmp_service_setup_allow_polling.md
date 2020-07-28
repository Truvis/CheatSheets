# SNMP Setup for sending information

## Linux
curl -o /usr/local/bin/distro https://gitlab.com/observium/distroscript/raw/master/distro

chmod +x /usr/local/bin/distro

snmpd.conf:

extend .1.3.6.1.4.1.2021.7890.1 distro /usr/local/bin/distro

extend .1.3.6.1.4.1.2021.7890.2 hardware /bin/cat /sys/devices/virtual/dmi/id/product_name

extend .1.3.6.1.4.1.2021.7890.3 vendor   /bin/cat /sys/devices/virtual/dmi/id/sys_vendor

extend .1.3.6.1.4.1.2021.7890.4 serial   /bin/cat /sys/devices/virtual/dmi/id/product_serial

extend uptime /bin/cat /proc/uptime

In some environments snmpd not have permission for read file /sys/devices/virtual/dmi/id/product_serial. Need to change file permission at boot by adding this command to /etc/rc.local: chmod 444 /sys/devices/virtual/dmi/id/product_serial

## Windows 2012 R2+

1. Log into your dedicated server using Remote Desktop
2. Click on Windows Key > Administrative Tools > Server Manager.
3. Click Manage >  Add Roles and Features.
4. Click Next > Next > Next > Next. Verify SNMP Services are installed.
5. Click Cancel. If SNMP is not installed, contact Support.
6. Click on Windows Key > Administrative Tools > Services.
7. Right-click on SNMP Service and click on Properties.
8. Click on the Security tab. 
9. Type your randomized 8 - 10 character connection string. Be sure to make it Read Only, not Read Write.

## Windows 10 1809+ 
1. Get-WindowsCapability -Online -Name "SNMP*"
2. Get-WindowsCapability -Online -Name "SNMP*"
3. Add-WindowsCapability -Online -Name "SNMP.Client~~~~0.0.1.0"

## ESXI 5.5
1. esxcli system snmp set --communities YOUR_STRING
2. esxcli system snmp set --enable true
3. esxcli network firewall ruleset set --ruleset-id snmp --allowed-all true
4. esxcli network firewall ruleset set --ruleset-id snmp --enabled true
5. /etc/init.d/snmpd restart

## ESXI 6.x
1. esxcli system snmp set -r
2. esxcli system snmp set -c YOUR_STRING
3. esxcli system snmp set -p 161
4. esxcli system snmp set -L "City, State, Country"
5. esxcli system snmp set -C noc@example.com
6. esxcli system snmp set -e yes



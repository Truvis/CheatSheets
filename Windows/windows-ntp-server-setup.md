net stop w32time
w32tm /config /syncfromflags:manual /manualpeerlist:"0.us.pool.ntp.org,1.us.pool.ntp.org,2.us.pool.ntp.org,3.us.pool.ntp.org"
w32tm /config /reliable:yes
net start w32time
w32tm /query /configuration
w32tm /query /status

set dhcp to set local ntp server as the time server

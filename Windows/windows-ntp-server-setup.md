1. net stop w32time
2. w32tm /config /syncfromflags:manual /manualpeerlist:"0.us.pool.ntp.org,1.us.pool.ntp.org,2.us.pool.ntp.org,3.us.pool.ntp.org"
3. w32tm /config /reliable:yes
4. net start w32time
5. w32tm /query /configuration
6. w32tm /query /status
7. set dhcp to set local ntp server as the time server


##### confirm current setting (follows are default settings)
PS C:\Users\Administrator> Get-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\w32time\TimeProviders\NtpServer" 

##### enable NTP Server feature
PS C:\Users\Administrator> Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\w32time\TimeProviders\NtpServer" -Name "Enabled" -Value 1 

# set [AnnounceFlags] to 5
- number means
- 0x00 : Not a time server
- 0x01 : Always time server
- 0x02 : Automatic time server
- 0x04 : Always reliable time server
- 0x08 : Automatic reliable time server
PS C:\Users\Administrator> Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\services\W32Time\Config" -Name "AnnounceFlags" -Value 5 

##### restart Windows Time service
PS C:\Users\Administrator> Restart-Service w32Time 

##### if Windows Firewall is running, allow NTP port
PS C:\Users\Administrator> New-NetFirewallRule `
-Name "NTP Server Port" `
-DisplayName "NTP Server Port" `
-Description 'Allow NTP Server Port' `
-Profile Any `
-Direction Inbound `
-Action Allow `
-Protocol UDP `
-Program Any `
-LocalAddress Any `
-LocalPort 123 

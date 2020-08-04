##### find hosts not using local NTP server
- source="/var/log/opnsense/{HOST}/opnsense.log" dest_port="123" src_ip="192.168.*" | stats values(dest_ip) as dest_ips by src_ip

##### Blocked outgoing connections by IP (graphable)
- index=main sourcetype="opnsense:filterlog" action=blocked src_ip!="192.168.2.2" src_ip!="192.168.2.3" src_ip="192.168.*" dest_ip!="192.168.*" | stats count(src_ip) by src_ip

##### Blocked out going connections by PORT (graphable)
- index=main sourcetype="opnsense:filterlog" action=blocked src_ip!="192.168.2.2" src_ip!="192.168.2.3" src_ip="192.168.*" dest_port!="53" dest_ip!="192.168.*"  | stats count(dest_port) by dest_port

##### Firewall Destination IP Most bytes (graphable)
- index=main sourcetype="opnsense:filterlog" | stats count(bytes) as TotalBytes by dest_ip

##### Filewall Source IP Most bytes (graphable)
- index=main sourcetype="opnsense:filterlog"  src_ip="192.168.*" | stats  count(bytes) as TotalBytes by src_ip

##### Search by country and region for stats (graphable)
- host="{FIREWALL}" dest_ip="{WAN}" action=* | iplocation src_ip | search Country = China | stats count by Country, Region, action

##### out going to countries from internal
- host="{FIREWALL}" src_ip="192.168.*" action=* | iplocation dest_ip | search Country = * | stats count by Country

#### events pre hour BY sourctype
- sourcetype="WinEventLog:Security" | bin _time span=1h | eval date_hour=strftime(_time, "%H") | stats count AS hits first(date_hour) AS date_hour BY _time | stats avg(hits) BY date_hour

#### events per hour by Windows EventLogs BY HOST
- sourcetype="WinEventLog:Security" EventCode=4673 | timechart span=1h count by host

#### events per hour by windows EventLogs BY EVENT TYPE
 - sourcetype="WinEventLog:Security" | timechart span=1h count by EventCode

### REFS:
- https://docs.splunksecurityessentials.com/content-detail/sser_malicious_command_line_executions/ (contains good queries all around)
- https://www.sans.org/reading-room/whitepapers/critical/finding-bad-splunk-37482

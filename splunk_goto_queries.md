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
- host="edge.internal.truvis.cat" dest_ip="96.58.127.84" action=* | iplocation src_ip | search Country = China | stats count by Country, Region, action

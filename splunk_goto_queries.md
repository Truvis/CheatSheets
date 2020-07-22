##### find hosts not using local NTP server
- source="/var/log/opnsense/{HOST}/opnsense.log" dest_port="123" src_ip="192.168.*" | stats values(dest_ip) as dest_ips by src_ip

##### Blocked outgoing connections by IP (graphable)
- index=main sourcetype="opnsense:filterlog" action=blocked src_ip!="192.168.2.2" src_ip!="192.168.2.3" src_ip="192.168.*" dest_ip!="192.168.*" | stats count(src_ip) by src_ip


##### Blocked out going connections by PORT (graphable)
- index=main sourcetype="opnsense:filterlog" action=blocked src_ip!="192.168.2.2" src_ip!="192.168.2.3" src_ip="192.168.*" dest_port!="53" dest_ip!="192.168.*"  | stats count(dest_port) by dest_port

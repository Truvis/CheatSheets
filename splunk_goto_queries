##### find hosts not using local NTP server
- source="/var/log/opnsense/edge.internal.truvis.cat/opnsense.log" dest_port="123" src_ip="192.168.*" | stats values(dest_ip) as dest_ips by src_ip


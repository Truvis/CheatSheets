### Windows 10
#### WinLogBeat
- cd "C:\Program Files\winlogbeat-7.9.0\" .\install-service-winlogbeat.ps1
- .\winlogbeat.exe setup--dashboards
- change localhost to IPs under winlogbeat.yml
- start service

### Linux
#### FileBeat
- curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.9.0-x86_64.rpm
- rpm -vi filebeat-7.9.0-x86_64.rpm
- change localhost to IPs under /etc/filebeat/filebeat.yml
- filebeat modules enable system apache nginx mysql auditd
- filebeat setup
- enable/start service


### REFS
- https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-installation-configuration.html

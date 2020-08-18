### Windows 10
- cd "C:\Program Files\winlogbeat-7.9.0\" .\install-service-winlogbeat.ps1
- .\winlogbeat.exe setup--dashboards
- change localhost to IPs under winlogbeat.yml
- start service

### Linux
- curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.9.0-linux-x86_64.tar.gz
- tar xzvf filebeat-7.9.0-linux-x86_64.tar.gz
- change localhost to IPs under winlogbeat.yml
- start service


### REFS
- https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-installation-configuration.html

# Windows
## Windows 10
### WinLogBeat
- cd "C:\Program Files\winlogbeat-7.9.0\" .\install-service-winlogbeat.ps1
- .\winlogbeat.exe setup--dashboards
- change localhost to IPs under winlogbeat.yml
- start service

# Linux
## CentOS 7
### FileBeat
- curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.9.0-x86_64.rpm
- rpm -vi filebeat-7.9.0-x86_64.rpm
- change localhost to IPs under /etc/filebeat/filebeat.yml
- filebeat modules enable system apache nginx mysql auditd
- filebeat setup
- enable/start service

### AuditBeat
- curl -L -O https://artifacts.elastic.co/downloads/beats/auditbeat/auditbeat-7.9.0-x86_64.rpm
- rpm -vi auditbeat-7.9.0-x86_64.rpm
- change localhost to IPs under /etc/auditbeat/auditbeat.yml
- auditbeat setup
- auditbeat setup -e
- enable/start service

### REFS
- https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-installation-configuration.html
- https://malware.news/t/monitoring-for-windows-event-logs-and-the-untold-story-of-proper-elk-integration/16816

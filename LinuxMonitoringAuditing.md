# Syslog

## LogRotate
/etc/logrotate.conf
Set how often logs are kept and when to rotate them
rotate 0 -- keep all the logs


## rsyslog vs syslog
rsyslog -- allows logging to remote and local

### /etc/rsyslog.conf 
syslog does not check or validate - use firewall for whitelisting.

service.message type {info, warning, alert...}

# journalD

stores logs as a binary -- they cant be modified












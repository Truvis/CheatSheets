- wget -O splunkforwarder-8.0.5-a1a6394cc5ae-Linux-x86_64.tgz 'https://www.splunk.com/bin/splunk/DownloadActivityServlet?architecture=x86_64&platform=linux&version=8.0.5&product=universalforwarder&filename=splunkforwarder-8.0.5-a1a6394cc5ae-Linux-x86_64.tgz&wget=true'
- tar xvzf splunkforwarder*.tgz -C /opt
- vi ~/.bashrc
- export SPLUNK_HOME="/opt/splunkforwarder"
- export PATH=$PATH:$SPLUNK_HOME/bin 
- exec bash
- splunk enable boot-start 
- cd $SPLUNK_HOME/bin ./splunk start
- vi $SPLUNK_HOME/etc/system/local/inputs.conf
- [monitor:///var/log/]
- ./splunk add forward-server host:9997
- splunk restart

### dont foward files
Add blacklist to not forward certain files
- blacklist = pihole*
- blacklist = access*

### inputs.conf - fine tuned for controlling indexs and sources when searching

```
[monitor:///var/log]
whitelist=(log$|messages|mesg$|cron$|acpid$|\.out)
blacklist=(\.gz$|\.zip$|\.bz2$|auth\.log|lastlog|secure|anaconda\.syslog)
index=osnix
sourcetype=syslog
disabled = 0

[monitor:///var/log/secure]
blacklist=(\.gz$|\.zip$|\.bz2$)
index=osnixsec
sourcetype=syslog
source=secure
disabled = 0

[monitor:///var/log/auth.log*]
blacklist=(\.gz$|\.zip$|\.bz2$)
index=osnixsec
sourcetype=syslog
disabled = 0

[monitor:///root/.bash_history]
sourcetype = bash_history
index = osnixbash
disabled = 0

[monitor:///home/.../.bash_history]
sourcetype = bash_history
index = osnixbash
disabled = 0
```



REFS:
- https://medium.com/@devopsprosiva/splunk-install-linux-universal-forwarder-3e115d51e751
- https://docs.splunk.com/Documentation/Splunk/8.0.5/AddASAsingle/InstallUF
- https://conf.splunk.com/files/2016/slides/behind-the-magnifying-glass-how-search-works.pdf
- https://conf.splunk.com/files/2016/slides/search-optimization.pdf

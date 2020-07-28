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

REFS:
- https://medium.com/@devopsprosiva/splunk-install-linux-universal-forwarder-3e115d51e751
- https://docs.splunk.com/Documentation/Splunk/8.0.5/AddASAsingle/InstallUF

- wget tgz
- tar xvzf splunkforwarder-<…>-Linux-x86_64.tgz -C /opt
- vi ~/.bashrc
- export SPLUNK_HOME="/opt/splunkforwarder"
- export PATH=$PATH:$SPLUNK_HOME/bin 
- exec bash
- splunk enable boot-start 
- cd $SPLUNK_HOME/bin ./splunk start
- vi $SPLUNK_HOME/etc/system/local/inputs.conf
- [monitor:///var/log]
- ./splunk add forward-server host:9997
- splunk restart

REFS:
- [https://medium.com/@devopsprosiva/splunk-install-linux-universal-forwarder-3e115d51e751]
- [https://docs.splunk.com/Documentation/Splunk/8.0.5/AddASAsingle/InstallUF]

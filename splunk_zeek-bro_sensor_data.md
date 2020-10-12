Follow the universal forwarder guide setup

```
vim /opt/splunkforwarder/etc/system/local/inputs.conf
```
- add the following
```
[default]
host = sensor

[monitor:///opt/zeek/logs/current/conn.log]
_TCP_ROUTING = *
index = zeek
sourcetype = zeek_conn

[monitor:///opt/zeek/logs/current/dns.log]
_TCP_ROUTING = *
index = zeek
sourcetype = zeek_dns

[monitor:///opt/zeek/logs/current/software.log]
_TCP_ROUTING = *
index = zeek
sourcetype = zeek_software

[monitor:///opt/zeek/logs/current/smtp.log]
_TCP_ROUTING = *
index = zeek
sourcetype = zeek_smtp

[monitor:///opt/zeek/logs/current/ssl.log]
_TCP_ROUTING = *
index = zeek
sourcetype = zeek_ssl

[monitor:///opt/zeek/logs/current/ssh.log]
_TCP_ROUTING = *
index = zeek
sourcetype = zeek_ssh

[monitor:///opt/zeek/logs/current/x509.log]
_TCP_ROUTING = *
index = zeek
sourcetype = zeek_x509

[monitor:///opt/zeek/logs/current/ftp.log]
_TCP_ROUTING = *
index = zeek
sourcetype = zeek_ftp

[monitor:///opt/zeek/logs/current/http.log]
_TCP_ROUTING = *
index = zeek
sourcetype = zeek_http

[monitor:///opt/zeek/logs/current/rdp.log]
_TCP_ROUTING = *
index = zeek
sourcetype = zeek_rdp

[monitor:///opt/zeek/logs/current/smb_files.log]
_TCP_ROUTING = *
index = zeek
sourcetype = zeek_smb_files

[monitor:///opt/zeek/logs/current/smb_mapping.log]
_TCP_ROUTING = *
index = zeek
sourcetype = zeek_smb_mapping

[monitor:///opt/zeek/logs/current/snmp.log]
_TCP_ROUTING = *
index = zeek
sourcetype = zeek_snmp

[monitor:///opt/zeek/logs/current/sip.log]
_TCP_ROUTING = *
index = zeek
sourcetype = zeek_sip

[monitor:///opt/zeek/logs/current/files.log]
_TCP_ROUTING = *
index = zeek
sourcetype = zeek_files
```



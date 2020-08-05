NOTES:
- index the collection name (becomes a name which is searchable within splunk)
- source is the name/file/stream/output like /var/log/messages (becomes a name which is searchable within splunk)
- sourcetype is the type like linux_syslog (becomes a name which is searchable within splunk)
- Searching index=a and sourcetype=b is like searching a.b
- It's best to always use both when possible to increase searching speed. 

### indexes
- logical separation of different types of data - e.g. if you're searching for linux logs, you don't need to search firewall logs, so you can specify index=linux.
- Role-based access restriction of data. Network guys don't need to see host logs, host guys don't need to see network logs.
- Varying retention requirements. You may need to retain firewall logs for a year, but host logs for 3 months. Different indexes allow you to have different retention policies.

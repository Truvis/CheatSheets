##### find hosts not using local NTP server
- source="/var/log/opnsense/{HOST}/opnsense.log" dest_port="123" src_ip="192.168.*" | stats values(dest_ip) as dest_ips by src_ip

##### Blocked outgoing connections by IP (graphable)
- index=main sourcetype="opnsense:filterlog" action=blocked src_ip!="192.168.2.2" src_ip!="192.168.2.3" src_ip="192.168.*" dest_ip!="192.168.*" | stats count(src_ip) by src_ip

##### Blocked out going connections by PORT (graphable)
- index=main sourcetype="opnsense:filterlog" action=blocked src_ip!="192.168.2.2" src_ip!="192.168.2.3" src_ip="192.168.*" dest_port!="53" dest_ip!="192.168.*"  | stats count(dest_port) by dest_port

##### Firewall Destination IP Most bytes (graphable)
- index=main sourcetype="opnsense:filterlog" | stats count(bytes) as TotalBytes by dest_ip

##### Filewall Source IP Most bytes (graphable)
- index=main sourcetype="opnsense:filterlog"  src_ip="192.168.*" | stats  count(bytes) as TotalBytes by src_ip

##### Search by country and region for stats (graphable)
- host="{FIREWALL}" dest_ip="{WAN}" action=* | iplocation src_ip | search Country = China | stats count by Country, Region, action

##### out going to countries from internal
- host="{FIREWALL}" src_ip="192.168.*" action=* | iplocation dest_ip | search Country = * | stats count by Country

#### events pre hour BY sourctype
- sourcetype="WinEventLog:Security" | bin _time span=1h | eval date_hour=strftime(_time, "%H") | stats count AS hits first(date_hour) AS date_hour BY _time | stats avg(hits) BY date_hour

#### events per hour by Windows EventLogs BY HOST
- sourcetype="WinEventLog:Security" EventCode=4673 | timechart span=1h count by host

#### events per hour by windows EventLogs BY EVENT TYPE
 - sourcetype="WinEventLog:Security" | timechart span=1h count by EventCode
 
#### Event Log clears in windows
- index=* (source="WinEventLog:Security" AND (EventCode=1102 OR EventCode=1100)) OR ((source="WinEventLog:System") AND EventCode=104) | stats count BY _time EventCode sourcetype host

#### Windows security daily domain activities
- sourcetype=WinEventLog:Security src_nt_domain!="NT AUTHORITY" EventCode=4720 OR EventCode=4726 OR EventCode=4738 OR EventCode=4767 OR EventCode=4781 OR EventCode=4727 OR EventCode=4730 OR EventCode=4731 OR EventCode=4734 OR EventCode=4735 OR EventCode=4737 OR EventCode=4744 OR EventCode=4745 OR EventCode=4748 OR EventCode=4749 OR EventCode=4750 OR EventCode=4753 OR EventCode=4754 OR EventCode=4755 OR EventCode=4758 OR EventCode=4759 OR EventCode=4760 OR EventCode=4763 OR EventCode=4764 OR EventCode=4728 OR EventCode=4729 OR EventCode=4732 OR EventCode=4733 OR EventCode=4746 OR EventCode=4747 OR EventCode=4751 OR EventCode=4752 OR EventCode=4756 OR EventCode=4757 OR EventCode=4761 OR EventCode=4762 | rex field=member_id "^\w+\W(?<ITS_Admin>\w*\s\w*\s\w*|\w+_\w+|\w*\s\w*|\w*)(\s\w+\W|\s)(?<Target_Account>.*\S)" | eval Target_Account=if(Target_Account="NONE_MAPPED", trim(member_dn, ITS_Admin), Target_Account) | table _time, EventCode, EventCodeDescription, src_nt_domain, ITS_Admin, Target_Account,src_nt_domain,msad_action,Group_Name | sort EventCodeDescription,ITS_Admin, Target_Account | rename ITS_Admin as "ITS Admin", src_nt_domain as "Source Domain"

#### Search Common EventCodes (EventID’s) for Suspicious Behavior
- source="wineventlog:security" user!="DWM-*" user!="UMFD-*" user!=SYSTEM user!="LOCAL SERVICE" user!="NETWORK SERVICE" user!="*$" user!="ANONYMOUS LOGON" user!="IUSR"
| eval Trigger=case(EventCode=516, "Audit Logs Modified",EventCode=517, "Audit Logs Modified",EventCode=612, "Audit Logs Modified",EventCode=623, "Audit Logs Modified",EventCode=806, "Audit Logs Modified",EventCode=807, "Audit Logs Modified",EventCode=1101, "Audit Logs Modified",EventCode=1102, "Audit Logs Modified",EventCode=4612, "Audit Logs Modified",EventCode=4621, "Audit Logs Modified",EventCode=4694, "Audit Logs Modified",EventCode=4695, "Audit Logs Modified",EventCode=4715, "Audit Logs Modified",EventCode=4719, "Audit Logs Modified",EventCode=4817, "Audit Logs Modified",EventCode=4885, "Audit Logs Modified",EventCode=4902, "Audit Logs Modified",EventCode=4906, "Audit Logs Modified",EventCode=4907, "Audit Logs Modified",EventCode=4912, "Audit Logs Modified", EventCode=642, "Account Modification",EventCode=646, "Account Modification",EventCode=685, "Account Modification",EventCode=4738, "Account Modification",EventCode=4742, "Account Modification",EventCode=4781, "Account Modification", EventCode=1102, "Audit Logs Cleared/Deleted",EventCode=517, "Audit Logs Cleared/Deleted", EventCode=628, "Passwords Changed",EventCode=627, "Passwords Changed",EventCode=4723, "Passwords Changed",EventCode=4724, "Passwords Changed", EventCode=528, "Successful Logons",EventCode=540, "Successful Logons",EventCode=4624, "Successful Logons", EventCode=4625, "Failed Logons",EventCode=529, "Failed Logons",EventCode=530, "Failed Logons",EventCode=531, "Failed Logons",EventCode=532, "Failed Logons",EventCode=533, "Failed Logons",EventCode=534, "Failed Logons",EventCode=535, "Failed Logons",EventCode=536, "Failed Logons",EventCode=537, "Failed Logons",EventCode=539, "Failed Logons", EventCode=576, "Escalation of Privileges",EventCode=4672, "Escalation of Privileges",EventCode=577, "Escalation of Privileges",EventCode=4673, "Escalation of Privileges",EventCode=578, "Escalation of Privileges",EventCode=4674, "Escalation of Privileges") | stats earliest(_time) as Initial_Occurrence latest(_time) as Latest_Occurrence values(user) as Users values(host) as Hosts count sparkline by Trigger | sort - count | convert ctime(Initial_Occurrence) ctime(Latest_Occurrence)

#### Active Directory Password change attempts
- source="WinEventLog:Security" "EventCode=4723" src_user!="*$" src_user!="_svc_*" | eval daynumber=strftime(_time,"%Y-%m-%d") | chart count by daynumber, status | eval daynumber = mvindex(split(daynumber,"-"),2)

#### Security Access granted to an Account
- sourcetype="WinEventLog:Security" EventCode=4717 | eval Date=strftime(_time, "%Y/%m/%d") | stats count by src_user, user, Access_Right, Date, Keywords |rename src_user as "Source Account" | rename user as "Target Account" | rename Access_Right as "New Rights Granted"

#### System Security Access Removed from Account
- sourcetype="WinEventLog:Security" EventCode=4718 | eval Date=strftime(_time, "%Y/%m/%d") | stats count by src_user, user, Access_Right, Date, Keywords |rename src_user as "Source Account" | rename user as "Target Account" | rename Access_Right as "Rights Removed"

#### Timechart of the status of an Locked Out Account
- 	sourcetype="WinEventLog:Security" EventCode=4625 AND Status=0xC0000234 | timechart count by user | sort -count


### REFS:
- https://docs.splunksecurityessentials.com/content-detail/sser_malicious_command_line_executions/ (contains good queries all around)
- https://www.sans.org/reading-room/whitepapers/critical/finding-bad-splunk-37482

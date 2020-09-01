# Windows Server 2008, Server 2008 R2, Server 2012, Server 2012 R2, and Server 2016
### Computer Configuration > Policies > Windows Settings > Security Settings > Local Policy > Audit Policy.
1. Enable both Success and Failure auditing of the following policy settings:
- Audit account logon events
- Audit account management
- Audit directory service access
- Audit logon events
- Audit object access
- Audit policy change
- Audit privilege use
- Audit system events

### tweaks:
- auditpol /set /subcategory:"Filtering Platform Packet Drop" /success:disable /failure:disable
- auditpol /set /subcategory:"Filtering Platform Connection" /success:disable /failure:disable
- host=* category="Filtering Platform Connection" --- can be a little loud in the background. 


### refs:
- https://docs.microsoft.com/en-us/windows-server/identity/ad-ds/plan/appendix-l--events-to-monitor
- https://docs.microsoft.com/en-us/windows-server/identity/ad-ds/plan/security-best-practices/audit-policy-recommendations
- https://malwarearchaeology.squarespace.com/cheat-sheets
- https://docs.splunk.com/Documentation/Splunk/latest/Data/MonitorfilesystemchangesonWindows

# Collect Windows Filtering Platform (WFP) events in SEM
## Alert Name	Windows Event ID
- TCPTrafficAudit	5152, 5154, 5156, 5157, 5158, 5159
- IPTrafficAudit	5152, 5154, 5156, 5157, 5158, 5159
- UDPTrafficAudit	5152, 5154, 5156, 5157, 5158, 5159
- ICMPTrafficAudit	5152, 5156, 5157, 5158, 5159
- RoutingTrafficAudit	5152, 5156
- PPTPTrafficAudit	5152

## Event ID	Brief Description
- 5152	Windows Filtering Platform blocked a packet
- 5154	Windows Filtering Platform permitted an application or service to listen on a port for incoming connections
- 5156	Windows Filtering Platform allowed a connection
- 5157	Windows Filtering Platform blocked a connection
- 5158	Windows Filtering Platform permitted a bind to a local port
- 5159	Windows Filtering Platform blocked a bind to a local port

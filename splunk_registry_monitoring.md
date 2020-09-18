Still a work in progress. Rough draft Idea.

## infos

```
\\?.* Can have subkeys, but does not need to.
\\\\?.* Must have subkeys.
\\[^\\]* No Subkey, only values.
```

```
[WinRegMon]
disabled = 0
hive=NULL
proc = .*
type = rename|set|delete|create
baseline = 1
baseline_interval = 3000

[WinRegMon://reg_1]
hive=\\REGISTRY\\MACHINE\\CurrentControlSet\\Services\\UsbStor\\?.*
[WinRegMon://reg_2]
hive=\\REGISTRY\\MACHINE\\Software\\Classes\\AllFileSystemObjects\\ShellEx\\?.*
[WinRegMon://reg_3]
hive=\\REGISTRY\\MACHINE\\Software\\Classes\\CLSID\\?.*
type = create|set
[WinRegMon://reg_4]
hive=\\REGISTRY\\MACHINE\\Software\\Classes\\CLSID\\\{083863F1-70DE-11d0-BD40-00A0C911CE86\}\\Instance\\?.*
[WinRegMon://reg_5]
hive=\\REGISTRY\\MACHINE\\Software\\Classes\\Directory\\ShellEx\\?.*
[WinRegMon://reg_6]
hive=\\REGISTRY\\MACHINE\\Software\\Classes\\Folder\\ShellEx\\?.*
[WinRegMon://reg_7]
hive=\\REGISTRY\\MACHINE\\Software\\Classes\\Htmlfile\\Shell\\Open\\Command\\?.*
[WinRegMon://reg_8]
hive=\\REGISTRY\\MACHINE\\Software\\Classes\\Protocols\\Filter\\?.*
[WinRegMon://reg_9]
hive=\\REGISTRY\\MACHINE\\Software\\Classes\\Protocols\\Handler\\?.*
[WinRegMon://reg_10]
hive=\\REGISTRY\\MACHINE\\Software\\Classes\\.*\\ShellEx\\?.*
[WinRegMon://reg_11]
hive=\\REGISTRY\\MACHINE\\Software\\Clients\\Mail\\?.*
[WinRegMon://reg_12]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\Active Setup\\Installed Components\\?.*
[WinRegMon://reg_13]
hive=\\REGISTRY\\MACHINE\\SOFTWARE\\Microsoft\\Cryptography\\OID\\?.*
[WinRegMon://reg_14]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\Cryptography\\OID\\EncodingType 0\\CryptSIPDllGetSignedDataMsg\\\{SIP Guid\}\\?.*
[WinRegMon://reg_15]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\Cryptography\\OID\\EncodingType 0\\CryptSIPDllVerifyIndirectData\\\{SIP Guid\}\\?.*
[WinRegMon://reg_16]
hive=\\REGISTRY\\MACHINE\\SOFTWARE\\Microsoft\\Cryptography\\Providers\\Trust\\?.*
[WinRegMon://reg_17]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\Cryptography\\Providers\\Trust\\FinalPolicy\\\{SIP Guid\}\\?.*
[WinRegMon://reg_18]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\EnterpriseCertificates\\AuthRoot\\Certificates\\?.*
[WinRegMon://reg_19]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\EnterpriseCertificates\\CA\\Certificates\\?.*
[WinRegMon://reg_20]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\EnterpriseCertificates\\Root\\Certificates\\?.*
[WinRegMon://reg_21]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\Internet Explorer\\Toolbar\\?.*
[WinRegMon://reg_22]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\.NETFramework\\?.*
[WinRegMon://reg_23]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\Office\\Excel\\Addins\\?.*
type = create|set
[WinRegMon://reg_24]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\Office\\Outlook\\Addins\\?.*
type = create|set
[WinRegMon://reg_25]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\Office\\PowerPoint\\Addins\\?.*
type = create|set
[WinRegMon://reg_26]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\Office\\Word\\Addins\\?.*
type = create|set
[WinRegMon://reg_27]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\SystemCertificates\\AuthRoot\\Certificates\\?.*
[WinRegMon://reg_28]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\SystemCertificates\\CA\\Certificates\\?.*
[WinRegMon://reg_29]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\SystemCertificates\\Root\\Certificates\\?.*
[WinRegMon://reg_30]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\Terminal Server Client\\?.*
[WinRegMon://reg_31]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\VBA\\Monitors\\?.*
[WinRegMon://reg_32]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\WBEM\\CIMOM\\[^\\]*
[WinRegMon://reg_33]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\WBEM\\ESS\\?.*
type = create|set
[WinRegMon://reg_34]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\Windows\\CurrentVersion\\App Paths\\?.*
[WinRegMon://reg_35]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\Windows\\CurrentVersion\\Authentication\\Credential Provider Filters\\?.*
[WinRegMon://reg_36]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\Windows\\CurrentVersion\\Authentication\\Credential Providers\\?.*
[WinRegMon://reg_37]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\Windows\\CurrentVersion\\Authentication\\PLAP Providers\\?.*
[WinRegMon://reg_38]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\Windows\\CurrentVersion\\Explorer\\Browser Helper Objects\\?.*
[WinRegMon://reg_39]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\Windows\\CurrentVersion\\Explorer\\ShellExecuteHooks\\?.*
[WinRegMon://reg_40]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\Windows\\CurrentVersion\\Explorer\\ShellIconOverlayIdentifiers\\?.*
[WinRegMon://reg_41]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\Windows\\CurrentVersion\\Explorer\\ShellServiceObjects\\?.*
[WinRegMon://reg_42]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\Windows\\CurrentVersion\\Explorer\\TBDEn\\?.*
[WinRegMon://reg_43]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\Windows\\CurrentVersion\\Group Policy\\Scripts\\?.*
[WinRegMon://reg_44]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\Windows\\CurrentVersion\\Policies\\Explorer\\Run\\?.*
[WinRegMon://reg_45]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\Windows\\CurrentVersion\\Policies\\System\\?.*
[WinRegMon://reg_46]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\Windows\\CurrentVersion\\Run\\?.*
[WinRegMon://reg_47]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\Windows\\CurrentVersion\\RunOnce\\?.*
[WinRegMon://reg_48]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\Windows\\CurrentVersion\\Shell Extensions\\?.*
[WinRegMon://reg_49]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\Windows NT\\CurrentVersion\\Accessibility\\ATs\\[^\\]*
[WinRegMon://reg_50]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\Windows NT\\CurrentVersion\\AeDebug\\?.*
[WinRegMon://reg_51]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\Windows NT\\CurrentVersion\\Drivers32\\?.*
[WinRegMon://reg_52]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\Windows NT\\CurrentVersion\\Font Drivers\\?.*
[WinRegMon://reg_53]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\Windows NT\\CurrentVersion\\Image File Execution Options\\?.*
[WinRegMon://reg_54]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\Windows NT\\CurrentVersion\\SilentProcessExit\\?.*
[WinRegMon://reg_55]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\Windows NT\\CurrentVersion\\SystemRestore\\?.*
[WinRegMon://reg_56]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\Windows NT\\CurrentVersion\\Windows\\?.*
[WinRegMon://reg_57]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\Windows NT\\CurrentVersion\\Windows\\IconServiceLib\\?.*
[WinRegMon://reg_58]
hive=\\REGISTRY\\MACHINE\\Software\\Microsoft\\Windows NT\\CurrentVersion\\Winlogon\\?.*
[WinRegMon://reg_59]
hive=\\REGISTRY\\MACHINE\\Software\\Policies\\Microsoft\\PowerShell\\?.*
[WinRegMon://reg_60]
hive=\\REGISTRY\\MACHINE\\Software\\Policies\\Microsoft\\SystemCertificates\\AuthRoot\\Certificates\\?.*
[WinRegMon://reg_61]
hive=\\REGISTRY\\MACHINE\\Software\\Policies\\Microsoft\\SystemCertificates\\CA\\Certificates\\?.*
[WinRegMon://reg_62]
hive=\\REGISTRY\\MACHINE\\Software\\Policies\\Microsoft\\SystemCertificates\\Root\\Certificates\\?.*
[WinRegMon://reg_63]
hive=\\REGISTRY\\MACHINE\\Software\\Policies\\Microsoft\\Windows\\System\\Scripts\\?.*
[WinRegMon://reg_64]
hive=\\REGISTRY\\MACHINE\\Software\\Wow6432Node\\Classes\\AllFileSystemObjects\\ShellEx\\?.*
[WinRegMon://reg_65]
hive=\\REGISTRY\\MACHINE\\Software\\Wow6432Node\\Classes\\CLSID\\\{083863F1-70DE-11d0-BD40-00A0C911CE86\}\\Instance\\?.*
[WinRegMon://reg_66]
hive=\\REGISTRY\\MACHINE\\Software\\Wow6432Node\\Classes\\Directory\\ShellEx\\?.*
[WinRegMon://reg_67]
hive=\\REGISTRY\\MACHINE\\Software\\Wow6432Node\\Classes\\Folder\\ShellEx\\?.*
[WinRegMon://reg_68]
hive=\\REGISTRY\\MACHINE\\Software\\Wow6432Node\\Classes\\.*\\ShellEx\\?.*
[WinRegMon://reg_69]
hive=\\REGISTRY\\MACHINE\\Software\\Wow6432Node\\Microsoft\\Active Setup\\Installed Components\\?.*
[WinRegMon://reg_70]
hive=\\REGISTRY\\MACHINE\\SOFTWARE\\WOW6432Node\\Microsoft\\Cryptography\\OID\\?.*
[WinRegMon://reg_71]
hive=\\REGISTRY\\MACHINE\\Software\\Wow6432Node\\Microsoft\\Cryptography\\OID\\EncodingType 0\\CryptSIPDllGetSignedDataMsg\\\{SIP Guid\}\\?.*
[WinRegMon://reg_72]
hive=\\REGISTRY\\MACHINE\\Software\\Wow6432Node\\Microsoft\\Cryptography\\OID\\EncodingType 0\\CryptSIPDllVerifyIndirectData\\\{SIP Guid\}\\?.*
[WinRegMon://reg_73]
hive=\\REGISTRY\\MACHINE\\SOFTWARE\\WOW6432Node\\Microsoft\\Cryptography\\Providers\\Trust\\?.*
[WinRegMon://reg_74]
hive=\\REGISTRY\\MACHINE\\Software\\Wow6432Node\\Microsoft\\Cryptography\\Providers\\Trust\\FinalPolicy\\\{SIP Guid\}\\?.*
[WinRegMon://reg_75]
hive=\\REGISTRY\\MACHINE\\Software\\Wow6432Node\\Microsoft\\.NETFramework\\?.*
[WinRegMon://reg_76]
hive=\\REGISTRY\\MACHINE\\Software\\Wow6432Node\\Microsoft\\Office\\Excel\\Addins\\?.*
[WinRegMon://reg_77]
hive=\\REGISTRY\\MACHINE\\Software\\Wow6432Node\\Microsoft\\Office\\Outlook\\Addins\\?.*
[WinRegMon://reg_78]
hive=\\REGISTRY\\MACHINE\\Software\\Wow6432Node\\Microsoft\\Office\\PowerPoint\\Addins\\?.*
[WinRegMon://reg_79]
hive=\\REGISTRY\\MACHINE\\Software\\Wow6432Node\\Microsoft\\Office\\Word\\Addins\\?.*
[WinRegMon://reg_80]
hive=\\REGISTRY\\MACHINE\\Software\\Wow6432Node\\Microsoft\\Windows\\CurrentVersion\\Explorer\\ShellExecuteHooks\\?.*
[WinRegMon://reg_81]
hive=\\REGISTRY\\MACHINE\\Software\\Wow6432Node\\Microsoft\\Windows\\CurrentVersion\\Explorer\\ShellIconOverlayIdentifiers\\?.*
[WinRegMon://reg_82]
hive=\\REGISTRY\\MACHINE\\Software\\Wow6432Node\\Microsoft\\Windows\\CurrentVersion\\Explorer\\ShellServiceObjects\\?.*
[WinRegMon://reg_83]
hive=\\REGISTRY\\MACHINE\\Software\\Wow6432Node\\Microsoft\\Windows\\CurrentVersion\\Run\\?.*
[WinRegMon://reg_84]
hive=\\REGISTRY\\MACHINE\\Software\\Wow6432Node\\Microsoft\\Windows\\CurrentVersion\\RunOnce\\?.*
[WinRegMon://reg_85]
hive=\\REGISTRY\\MACHINE\\Software\\Wow6432Node\\Microsoft\\Windows NT\\CurrentVersion\\AeDebug\\?.*
[WinRegMon://reg_86]
hive=\\REGISTRY\\MACHINE\\Software\\Wow6432Node\\Microsoft\\Windows NT\\CurrentVersion\\Drivers32\\?.*
[WinRegMon://reg_87]
hive=\\REGISTRY\\MACHINE\\Software\\Wow6432Node\\Microsoft\\Windows NT\\CurrentVersion\\Image File Execution Options\\?.*
[WinRegMon://reg_88]
hive=\\REGISTRY\\MACHINE\\System\\CurrentControlSet\\Control\\[^\\]*
[WinRegMon://reg_89]
hive=\\REGISTRY\\MACHINE\\System\\CurrentControlSet\\Control\\Citrix\\.*
[WinRegMon://reg_90]
hive=\\REGISTRY\\MACHINE\\System\\CurrentControlSet\\Control\\CrashControl\\?.*
[WinRegMon://reg_91]
hive=\\REGISTRY\\MACHINE\\System\\CurrentControlSet\\Control\\Lsa\\[^\\]*
[WinRegMon://reg_92]
hive=\\REGISTRY\\MACHINE\\System\\CurrentControlSet\\Control\\NetworkProvider\\Order\\?.*
[WinRegMon://reg_93]
hive=\\REGISTRY\\MACHINE\\System\\CurrentControlSet\\Control\\Print\\Monitors\\?.*
[WinRegMon://reg_94]
hive=\\REGISTRY\\MACHINE\\System\\CurrentControlSet\\Control\\SafeBoot\\[^\\]*
[WinRegMon://reg_95]
hive=\\REGISTRY\\MACHINE\\System\\CurrentControlSet\\Control\\SecurityProviders\\SecurityProviders\\[^\\]*
[WinRegMon://reg_96]
hive=\\REGISTRY\\MACHINE\\System\\CurrentControlSet\\Control\\SecurityProviders\\SecurityProviders\\WDigest\\[^\\]*
[WinRegMon://reg_97]
hive=\\REGISTRY\\MACHINE\\System\\CurrentControlSet\\Control\\Session Manager\\?.*
[WinRegMon://reg_98]
hive=\\REGISTRY\\MACHINE\\System\\CurrentControlSet\\Control\\Session Manager\\AppCertDlls\\?.*
[WinRegMon://reg_99]
hive=\\REGISTRY\\MACHINE\\System\\CurrentControlSet\\Control\\Session Manager\\Environment\\?.*
[WinRegMon://reg_100]
hive=\\REGISTRY\\MACHINE\\System\\CurrentControlSet\\Control\\Terminal Server\\AddIns\\[^\\]*
[WinRegMon://reg_101]
hive=\\REGISTRY\\MACHINE\\System\\CurrentControlSet\\Control\\Terminal Server\\Wds\\rdpwd\\[^\\]*
[WinRegMon://reg_102]
hive=\\REGISTRY\\MACHINE\\System\\CurrentControlSet\\Control\\Terminal Server\\Wds\\rdpwd\\StartupPrograms\\?.*
[WinRegMon://reg_103]
hive=\\REGISTRY\\MACHINE\\System\\CurrentControlSet\\services\\NTDS\\?.*
[WinRegMon://reg_104]
hive=\\REGISTRY\\MACHINE\\System\\CurrentControlSet\\Services\\RemoteAccess\\?.*
[WinRegMon://reg_105]
hive=\\REGISTRY\\MACHINE\\System\\CurrentControlSet\\Services\\SysmonDrv\\?.*
[WinRegMon://reg_106]
hive=\\REGISTRY\\MACHINE\\System\\CurrentControlSet\\Services\\(?!(tcpip)|(device lock))[^\\]*$
type = create|set
[WinRegMon://reg_107]
hive=\\REGISTRY\\MACHINE\\System\\CurrentControlSet\\Services\\WinSock2\\?.*
[WinRegMon://reg_108]
hive=\\REGISTRY\\USER\\.*\\Control Panel\\Desktop\\[^\\]*
[WinRegMon://reg_109]
hive=\\REGISTRY\\USER\\\.DEFAULT\\Control Panel\\Desktop\\[^\\]*
[WinRegMon://reg_110]
hive=\\REGISTRY\\USER\\\.DEFAULT\\Software\\Microsoft\\Internet Explorer\\UrlSearchHooks\\?.*
[WinRegMon://reg_111]
hive=\\REGISTRY\\USER\\\.DEFAULT\\Software\\Microsoft\\Office\\Outlook\\Addins\\?.*
[WinRegMon://reg_112]
hive=\\REGISTRY\\USER\\\.DEFAULT\\Software\\Microsoft\\Office\\PowerPoint\\Addins\\?.*
[WinRegMon://reg_113]
hive=\\REGISTRY\\USER\\\.DEFAULT\\Software\\Microsoft\\Office\\Word\\Addins\\?.*
[WinRegMon://reg_114]
hive=\\REGISTRY\\USER\\\.DEFAULT\\Software\\Microsoft\\Windows\\CurrentVersion\\Run\\?.*
[WinRegMon://reg_115]
hive=\\REGISTRY\\USER\\\.DEFAULT\\Software\\Microsoft\\Windows\\CurrentVersion\\RunOnce\\?.*
[WinRegMon://reg_116]
hive=\\REGISTRY\\USER\\.*\\Environment\\[^\\]*
[WinRegMon://reg_117]
hive=\\REGISTRY\\USER\\.*\\Software\\ALPS\\?.*
[WinRegMon://reg_118]
hive=\\REGISTRY\\USER\\.*\\Software\\Classes\\CLSID\\?.*
[WinRegMon://reg_119]
hive=\\REGISTRY\\USER\\.*\\Software\\Classes\\exefile\\shell\\runas\\command\\isolatedCommand\\?.*
[WinRegMon://reg_120]
hive=\\REGISTRY\\USER\\.*\\Software\\Classes\\mscfile\\shell\\open\\command\\?.*
[WinRegMon://reg_121]
hive=\\REGISTRY\\USER\\.*\\Software\\Classes\\Wow6432Node\\CLSID\\\{BCDE0395-E52F-467C-8E3D-C4579291692E\}\\?.*
[WinRegMon://reg_122]
hive=\\REGISTRY\\USER\\.*\\Software\\Microsoft\\CTF\\?.*
[WinRegMon://reg_123]
hive=\\REGISTRY\\USER\\.*\\Software\\Microsoft\\Internet Explorer\\UrlSearchHooks\\?.*
[WinRegMon://reg_124]
hive=\\REGISTRY\\USER\\.*\\Software\\Microsoft\\MultiMedia\\?.*
[WinRegMon://reg_125]
hive=\\REGISTRY\\USER\\.*\\Software\\Microsoft\\Office\\Outlook\\Addins\\?.*
[WinRegMon://reg_126]
hive=\\REGISTRY\\USER\\.*\\Software\\Microsoft\\Office\\PowerPoint\\Addins\\?.*
[WinRegMon://reg_127]
hive=\\REGISTRY\\USER\\.*\\Software\\Microsoft\\Office Test\\?.*
[WinRegMon://reg_128]
hive=\\REGISTRY\\USER\\.*\\Software\\Microsoft\\Office\\.*\\Word\\?.*
[WinRegMon://reg_129]
hive=\\REGISTRY\\USER\\.*\\Software\\Microsoft\\Office\\Word\\Addins\\?.*
[WinRegMon://reg_130]
hive=\\REGISTRY\\USER\\.*\\Software\\Microsoft\\SystemCertificates\\AuthRoot\\Certificates\\?.*
[WinRegMon://reg_131]
hive=\\REGISTRY\\USER\\.*\\Software\\Microsoft\\SystemCertificates\\CA\\Certificates\\?.*
[WinRegMon://reg_132]
hive=\\REGISTRY\\USER\\.*\\Software\\Microsoft\\SystemCertificates\\Root\\Certificates\\?.*
[WinRegMon://reg_133]
hive=\\REGISTRY\\USER\\.*\\Software\\Microsoft\\Windows\\CurrentVersion\\App Paths\\?.*
[WinRegMon://reg_134]
hive=\\REGISTRY\\USER\\.*\\Software\\Microsoft\\Windows\\CurrentVersion\\Control Panel\\Cpls\\?.*
[WinRegMon://reg_135]
hive=\\REGISTRY\\USER\\.*\\Software\\Microsoft\\Windows\\CurrentVersion\\Explorer\\?.*
[WinRegMon://reg_136]
hive=\\REGISTRY\\USER\\.*\\Software\\Microsoft\\Windows\\CurrentVersion\\Explorer\\FileExts\\?.*
[WinRegMon://reg_137]
hive=\\REGISTRY\\USER\\.*\\Software\\Microsoft\\Windows\\CurrentVersion\\Policies\\Explorer\\Run\\?.*
[WinRegMon://reg_138]
hive=\\REGISTRY\\USER\\.*\\Software\\Microsoft\\Windows\\CurrentVersion\\Run\\?.*
[WinRegMon://reg_139]
hive=\\REGISTRY\\USER\\.*\\Software\\Microsoft\\Windows\\CurrentVersion\\RunOnce\\?.*
[WinRegMon://reg_140]
hive=\\REGISTRY\\USER\\.*\\Software\\Microsoft\\Windows\\CurrentVersion\\Shell Extensions\\Cached\\?.*
[WinRegMon://reg_141]
hive=\\REGISTRY\\USER\\.*\\Software\\Microsoft\\Windows NT\\CurrentVersion\\Accessibility\\[^\\]*
[WinRegMon://reg_142]
hive=\\REGISTRY\\USER\\.*\\Software\\Microsoft\\Windows NT\\CurrentVersion\\AppCompatFlags\\Compatibility Assistant\\?.*
[WinRegMon://reg_143]
hive=\\REGISTRY\\USER\\.*\\Software\\Nico Mak Computing\\?.*
[WinRegMon://reg_144]
hive=\\REGISTRY\\USER\\.*\\Software\\Policies\\Microsoft\\SystemCertificates\\AuthRoot\\Certificates\\?.*
[WinRegMon://reg_145]
hive=\\REGISTRY\\USER\\.*\\Software\\Policies\\Microsoft\\SystemCertificates\\CA\\Certificates\\?.*
[WinRegMon://reg_146]
hive=\\REGISTRY\\USER\\.*\\Software\\Policies\\Microsoft\\SystemCertificates\\Root\\Certificates\\?.*
[WinRegMon://reg_147]
hive=\\REGISTRY\\USER\\.*\\Software\\Policies\\Microsoft\\Windows\\System\\Scripts\\?.*
[WinRegMon://reg_148]
hive=\\REGISTRY\\USER\\.*\\Software\\Synaptics\\?.*
[WinRegMon://reg_149]
hive=\\REGISTRY\\USER\\.*\\Software\\WinRAR\\?.*
```

# REFS:
- https://www.malwarearchaeology.com/s/Windows-Registry-Auditing-Cheat-Sheet-ver-Aug-2019.pdf
- https://static1.squarespace.com/static/552092d5e4b0661088167e5c/t/5a3187b4419202f0fb8b2dd1/1513195444728/Windows+Splunk+Logging+Cheat+Sheet+v2.2.pdf
- https://lolbas-project.github.io/
- https://www.hurricanelabs.com/splunk-tutorials/windows-event-log-filtering-design-in-splunk
- https://community.splunk.com/t5/Getting-Data-In/Monitoring-specific-keys-in-the-registry/td-p/338565
- https://docs.splunk.com/Documentation/Splunk/8.0.6/Data/MonitorWindowshostinformation
- https://resources.infosecinstitute.com/common-malware-persistence-mechanisms/#:~:text=These%20are%20located%20at%3A,Microsoft%5CWindows%5CCurrentVersion%5CRunServices
- https://attack.mitre.org/techniques/T1547/001/

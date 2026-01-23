# What does evil look like?

# [MITRE ATT&CK](https://attack.mitre.org/)
"knowledge base of adversary tactics and techniques based on real-world observations"

- categorizes malicious activity based on 3 components:
	1. Tactic (the why): the operational goal of the action
		- ex. "Initial Access", "Lateral Movement"
	2. Technique (the what): the method by which they conduct that action
		- ex. phishing, remote session hijacking, running a script
	3. Procedure (the how): the literal steps they use to perform it 
		- ex. hidden IFRAME in a webpage, scheduled task, RPC

None of these are comprehensive! But procedures are especially hard to exhaustively describe.

# How can we familiarize ourselves with it?
1. Attack simulations!
# [Atomic Red Team](https://github.com/redcanaryco/atomic-red-team)
"library of tests mapped to the [MITRE ATT&CK](https://attack.mitre.org/) framework"
## [Invoke-AtomicRedTeam](https://github.com/redcanaryco/invoke-atomicredteam)
"PowerShell module to execute tests as defined in the ... Atomic Red Team project"
### atomics: test files
`C:\AtomicRedTeam\atomics`
### useful commands
```powershell
Get-Help Invoke-AtomicTest

# general form of an atomic test
Invoke-AtomicTest <technique.[subtechnique]> -TestNumbers <n>

# try this out
Invoke-AtomicTest T1003.001 -TestNumbers 2 -ShowDetails

# handy flags
-ShowDetails
-CheckPrereqs
-GetPrereqs
```

# Where do we find its traces?
## Lab Setup
- one VM: victim + monitoring + attack

Windows 11 VM running:
- [Elasticsearch](https://www.elastic.co/elasticsearch) - log ingestion and search engine
- [Kibana](https://www.elastic.co/kibana) - visual interface to query logs
- [Sysmon](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon) - Windows service to monitor and log system activity
- Atomic Red Team
## Windows Event Logs
Path: `C:\Windows\System32\winevt\logs`
- stuff that happened on the system
- can read on live system with Windows Event Viewer
	- not suitable for forensic purposes (it sucks)
- categorized by a variety of event IDs
	- you'll never memorize them all!
	- [UltimateWindowsSecurity.com – Windows Security Log Events](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/default.aspx?i=j)
	- [Github – Awesome-event-ids](https://github.com/stuhli/awesome-event-ids)
### Sysmon
- adds several new events with considerable detail to the event log
- have to download (for now) and enable manually
![[sysmon-event-screen-optimized.png]]
### event categories we're ingesting (using Winlogbeat)
| Category    | Created By                                  | Examples                             |
| ----------- | ------------------------------------------- | ------------------------------------ |
| Application | applications and services                   | app errors and crashes               |
| System      | Windows system components and drivers       | hardware issues, OS errors           |
| Security    | authentication and user management services | logins, new user created             |
| Sysmon      | -                                           | process creation, network connection |
| PowerShell  | -                                           | module and script block logs         |
# Elasticsearch + Kibana
- our SIEM (Security Information and Event Management) platform
	- other tools include Splunk, IBM QRadar and Microsoft Sentinel
- general purpose search engine with powerful query language - Boolean searches
## KQL
"Kibana Query Language"

`winlog.channel:"Microsoft-Windows-Sysmon/Operational" AND event.code:1 AND process.name:mspaint.exe`

Common columns to add:
- @timestamp
- event.code
- winlog.channel
- user.name
- process.name
- source.ip
- destination.ip
- host.name

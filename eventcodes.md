# Common Event Codes
| Source                                   | Event IDs      | Description                                                        |
| ---------------------------------------- | -------------- | ------------------------------------------------------------------ |
| Security                                 | 4624           | An account was successfully logged on                              |
|                                          | 4672           | Special privileges assigned to new logon (user logged in as admin) |
|                                          | 4720/4726      | User account created/deleted                                       |
|                                          | 4728/4732/4756 | Member added to security-enabled group                             |
|                                          | 1102           | Security audit log cleared                                         |
| Microsoft-Windows-PowerShell/Operational | 4103, 4104     | module and script block logging                                    |
| Microsoft-Windows-Sysmon                 | 1              | Process creation                                                   |
|                                          | 3              | Network connection                                                 |
|                                          | 11             | File Create                                                        |
|                                          | 12, 33         | Registry events                                                    |
|                                          | 22             | DNS query                                                          |
| Microsoft-Windows-TaskScheduler          | 106            | Scheduled task created                                             |
| System                                   | 7045           | A new service was installed                                        |
| Microsoft-Windows-Windows Defender       | 1116           | Malware Detected                                                   |
|                                          | 1117           | Malware Action Taken                                               |
|                                          | 1118           | Malware Action Failed                                              |
|                                          | 1119           | Malware Action Critical Failure                                    |
# 4624 Details
https://docs.microsoft.com/en-us/windows/security/threat-protection/auditing/event-4624
*Subject*: who *reported* the logon
*New Logon*: who *logged on*
*Computer*: which system recorded the log
*Logon Type*:

| Logon Type | Logon Title         | Description                                                                           |
| ---------- | ------------------- | ------------------------------------------------------------------------------------- |
| **2**      | `Interactive`       | A user logged on to this computer, ex. via keyboard.                                  |
| **3**      | `Network`           | A user or computer logged on to this computer from the network, ex. SMB, P$ remoting  |
| **10**     | `RemoteInteractive` | A user logged on to this computer remotely using Terminal Services or Remote Desktop. |

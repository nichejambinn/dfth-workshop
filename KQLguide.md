# KQL Guide
## 1. Core Concepts (Winlogbeat)
When Winlogbeat ships Windows Event Logs to Elasticsearch, events typically land in indices like: `winlogbeat-*`

Key field families you will see:
- `event.*` – normalized event metadata
- `winlog.*` – Windows-specific fields (Event ID, channel, provider, message)
- `host.*` – system generating the event
- `user.*` – user context (when available)
- `process.*` – process metadata (often via Sysmon)
- `log.level` – severity (Information, Warning, Error)

---
## 2. Basic KQL Syntax

### Field equality
`event.code: 4624`
(Logon success)
### String match (exact)
`winlog.channel: "Security"`\
### Boolean logic
`winlog.channel: "Security" AND event.code: 4625`
(Failed logons)
### OR conditions
`event.code: (4624 or 4625)`
### NOT
`not user.name: "SYSTEM"`

---
## 3. Filtering by Log Type

### Application log
`winlog.channel: "Application"`
### System log
`winlog.channel: "System"`
### Security log
`winlog.channel: "Security"`

---
## 4. Common Beginner Queries (Windows Security)

### Successful logons
`winlog.channel: "Security" and event.code: 4624`

**Interesting fields to display**
- `@timestamp`
- `user.name`
- `user.domain`
- `winlog.event_data.LogonType`
- `source.ip`
- `host.name`

---
### Failed logons
`winlog.channel: "Security" and event.code: 4625`

**Interesting fields**
- `user.name`
- `winlog.event_data.FailureReason`
- `source.ip`
- `winlog.event_data.LogonType

---

### Account creation
`event.code: 4720`

**Interesting fields**
- `winlog.event_data.TargetUserName`
- `winlog.event_data.SubjectUserName`
- `host.name`

---
## 5. Searching Event Messages

### Keyword search (free text)
`winlog.message: "*powershell*"`
### Provider-specific
`winlog.provider_name: "Microsoft-Windows-Security-Auditing"`

---
## 6. Working with Sysmon via Winlogbeat

(Sysmon events are still Windows Event Logs)

### Process creation (Sysmon Event ID 1)
`winlog.provider_name: "Microsoft-Windows-Sysmon" and event.code: 1`

**Interesting fields**
- `process.name`
- `process.executable`
- `process.command_line`
- `user.name`
- `host.name`

---

### Network connections (Sysmon Event ID 3)
`event.code: 3 and winlog.provider_name: "Microsoft-Windows-Sysmon"`

**Interesting fields**
- `source.ip`
- `destination.ip`
- `destination.port`
- `process.name`

---

## 7. Select Fields to Display in Kibana

In **Discover**:
1. Run your KQL query
2. Use the **Fields sidebar** to:
    - Pin frequently used fields
    - Add them as columns
3. Save the view as a **Saved Search** for reuse

Tip for labs: start by pinning
```
@timestamp
event.code
winlog.channel
user.name
process.name
source.ip
destination.ip
host.name
```

# SIEM Analyst Cheat Sheet — SOC Analyst

A practical beginner-friendly reference for Security Information and Event Management (SIEM) and SOC alert investigation.

> Use SIEM tools only with authorized security data and systems.

## 1. What is a SIEM?

SIEM stands for **Security Information and Event Management**.

A SIEM collects and analyzes security-related data from many sources, such as:

- Windows Event Logs
- Linux logs
- Firewall logs
- DNS logs
- VPN logs
- Authentication logs
- Endpoint security tools
- Network devices
- Cloud services
- Applications

The SIEM helps a SOC analyst:

- Search logs
- Detect suspicious activity
- Correlate events
- Investigate alerts
- Build timelines
- Identify indicators of compromise (IOCs)
- Document incidents

---

## 2. Event vs Alert

### Event

An **event** is an activity recorded by a system.

Examples:

```text
User login
Process started
DNS request
Firewall connection
File created
Failed authentication
```

### Alert

An **alert** is generated when a rule or detection identifies activity that may require investigation.

Example:

```text
10 failed logins from one IP
        ↓
Detection rule
        ↓
SOC Alert
```

**SOC use:** An analyst investigates the alert and determines whether the activity is benign, suspicious, or malicious.

---

## 3. Common SIEM Data Sources

| Data source | Example information |
|---|---|
| Windows | Logons, processes, security events |
| Linux | Authentication and system logs |
| Firewall | Allowed/blocked connections |
| DNS | Domain queries |
| VPN | Remote access sessions |
| Endpoint/EDR | Processes, files, detections |
| Web server | HTTP requests |
| Cloud | Authentication and API activity |
| Network | Connections and traffic metadata |

**SOC use:** Correlating multiple sources can provide more context than investigating one log alone.

---

## 4. SIEM Investigation Questions

When investigating an alert, ask:

```text
What happened?
Who was involved?
Which host was involved?
When did it happen?
What IP address was involved?
What domain was involved?
What process or file was involved?
Was the activity expected?
Are other systems affected?
What evidence supports the alert?
```

---

# 5. Splunk Basics

Splunk is a SIEM/security analytics platform that can search and analyze machine-generated data.

Splunk searches commonly use **SPL (Search Processing Language)**.

### Search all events

```text
index=main
```

**SOC use:** Start searching data in a specific index.

### Search for a keyword

```text
index=main failed
```

**SOC use:** Find events containing a keyword.

### Search a field

```text
index=main user="admin"
```

**SOC use:** Investigate activity involving a specific user.

### Search an IP

```text
index=main src_ip="10.2.8.194"
```

**SOC use:** Investigate events associated with a source IP.

### Search a destination IP

```text
index=main dest_ip="8.8.8.8"
```

**SOC use:** Investigate communication with a destination.

### Count events

```text
index=main | stats count
```

**SOC use:** Understand how many events match a search.

### Count by source IP

```text
index=main | stats count by src_ip
```

**SOC use:** Find source IPs generating many events.

### Sort results

```text
index=main | sort - count
```

**SOC use:** Put high-count results first.

### Time filtering

```text
index=main earliest=-24h
```

**SOC use:** Search events from the last 24 hours.

> SPL syntax depends on the available fields and data model in the Splunk environment.

---

# 6. Microsoft Sentinel Basics

Microsoft Sentinel is Microsoft's cloud-native SIEM.

Sentinel commonly uses **KQL (Kusto Query Language)** for investigation.

### Search a table

```kusto
SecurityEvent
```

**SOC use:** Start investigating data in a Windows SecurityEvent table when that table exists in the environment.

### Limit results

```kusto
SecurityEvent
| take 10
```

**SOC use:** Quickly inspect sample events.

### Filter by Event ID

```kusto
SecurityEvent
| where EventID == 4625
```

**SOC use:** Investigate Windows failed logon events.

### Filter by IP

```kusto
SecurityEvent
| where IpAddress == "10.2.8.194"
```

**SOC use:** Investigate events associated with an IP address when that field is available.

### Count events

```kusto
SecurityEvent
| summarize count()
```

**SOC use:** Count matching events.

### Count by IP

```kusto
SecurityEvent
| summarize count() by IpAddress
```

**SOC use:** Identify IP addresses generating many matching events.

### Sort results

```kusto
SecurityEvent
| order by TimeGenerated desc
```

**SOC use:** View the newest events first.

> Table and field names vary depending on the Sentinel data connectors and workspace configuration.

---

# 7. Elastic Basics

Elastic Security is a security analytics platform built on the Elastic Stack.

Elastic commonly uses **Kibana** for searching, visualization, and investigation.

Important concepts include:

```text
Events
Fields
Indices / data streams
Queries
Dashboards
Detection rules
Alerts
Cases
```

Example search concepts:

```text
source.ip
destination.ip
user.name
process.name
host.name
event.code
```

Example query:

```text
source.ip: "10.2.8.194"
```

**SOC use:** Search events associated with a particular source IP.

Example:

```text
event.code: 4625
```

**SOC use:** Investigate a Windows event code when the data contains that field.

> Exact query syntax depends on the Elastic/Kibana version and query language being used.

---

# 8. Wazuh Basics

Wazuh is an open-source security platform commonly used for security monitoring, detection, and endpoint visibility.

Wazuh can provide information about:

- Authentication events
- File integrity
- System activity
- Vulnerabilities
- Malware-related detections
- Configuration changes
- Security alerts

Important concepts:

```text
Agent
Manager
Alerts
Rules
Decoders
File Integrity Monitoring
Vulnerability Detection
Dashboard
```

**SOC use:** Investigate endpoint alerts and correlate host activity.

---

# 9. IBM QRadar Basics

IBM QRadar is a SIEM platform used for security monitoring and event analysis.

Important concepts include:

```text
Events
Flows
Offenses
Rules
Log Sources
Ariel searches
```

### Offense

An **offense** represents a security investigation generated from correlated activity.

**SOC use:** Analysts can investigate the events and flows contributing to an offense.

### Log Source

A log source is a system or application sending security data to QRadar.

**SOC use:** Identify where the evidence originated.

---

# 10. Correlation

Correlation means connecting multiple events to understand a larger activity pattern.

Example:

```text
Failed login
      ↓
Successful login
      ↓
New process starts
      ↓
Outbound network connection
      ↓
Suspicious DNS query
```

Individually, each event may have an innocent explanation.

Together, they may require deeper investigation.

**SOC use:** Correlation helps reduce isolated-event thinking and provides context.

---

# 11. IOC Investigation

IOC = **Indicator of Compromise**.

Common IOCs include:

```text
IP address
Domain
URL
File hash
Email address
Filename
Process name
```

Example investigation:

```text
Suspicious IP
     ↓
Search SIEM
     ↓
Find affected hosts
     ↓
Find affected users
     ↓
Check timestamps
     ↓
Check processes
     ↓
Check DNS activity
     ↓
Build timeline
```

**Important:** An IOC is not automatically malicious. Validate it using context and additional evidence.

---

# 12. Alert Triage

Alert triage is the process of reviewing an alert and deciding what investigation is needed.

### Step 1 — Read the alert

Record:

```text
Alert name
Time
Host
User
Source IP
Destination IP
Process
File
Detection rule
```

### Step 2 — Check context

Ask:

```text
Is this normal for the user?
Is this normal for the host?
Is the process expected?
Is the destination expected?
Has this happened before?
```

### Step 3 — Search related events

Search for:

```text
Same user
Same host
Same IP
Same domain
Same process
Same file hash
Nearby timestamps
```

### Step 4 — Determine severity

Use the organization's documented severity criteria.

Consider:

```text
Impact
Confidence
Scope
Asset importance
User importance
Evidence of compromise
```

### Step 5 — Document

Record:

```text
Evidence
Timeline
Actions
Findings
Uncertainties
Next steps
```

---

# 13. Useful SIEM Investigation Fields

Common fields include:

| Field | Meaning |
|---|---|
| `timestamp` / `TimeGenerated` | When the event occurred |
| `host` / `host.name` | Computer involved |
| `user` / `user.name` | User involved |
| `src_ip` / `source.ip` | Source IP |
| `dest_ip` / `destination.ip` | Destination IP |
| `src_port` | Source port |
| `dest_port` | Destination port |
| `process.name` | Process name |
| `process.pid` | Process ID |
| `file.name` | File name |
| `file.hash` | File hash |
| `domain` | Domain involved |
| `event.code` | Event identifier |
| `action` | Action performed |
| `status` | Result/status |

> Exact field names vary between SIEM products and data sources.

---

# 14. SIEM Investigation Timeline

A timeline helps connect events.

Example:

```text
10:01:12
Failed login
        ↓
10:02:04
Successful login
        ↓
10:03:15
PowerShell process starts
        ↓
10:04:22
DNS query to unusual domain
        ↓
10:04:30
Outbound network connection
        ↓
10:05:10
Suspicious file created
```

**SOC use:** A timeline helps an analyst understand the sequence of activity.

---

# Quick SIEM Reference

| Task | Example |
|---|---|
| Search Splunk index | `index=main` |
| Search Splunk keyword | `index=main failed` |
| Search Splunk user | `index=main user="admin"` |
| Count Splunk events | `index=main \| stats count` |
| Count Splunk by IP | `index=main \| stats count by src_ip` |
| Search Sentinel table | `SecurityEvent` |
| Sample Sentinel events | `SecurityEvent \| take 10` |
| Sentinel failed logons | `SecurityEvent \| where EventID == 4625` |
| Count Sentinel events | `SecurityEvent \| summarize count()` |
| Elastic source IP | `source.ip: "10.2.8.194"` |
| Elastic event code | `event.code: 4625` |
| Wazuh | Investigate agents, alerts, rules, and endpoint activity |
| QRadar | Investigate offenses, events, flows, and log sources |

---

# SIEM Investigation Flow

```text
🚨 SIEM Alert
      ↓
Read alert details
      ↓
Identify host + user + time
      ↓
Identify IP / domain / process / file
      ↓
Search related events
      ↓
Check authentication activity
      ↓
Check endpoint activity
      ↓
Check network activity
      ↓
Check DNS activity
      ↓
Check file/hash information
      ↓
Correlate events
      ↓
Build timeline
      ↓
Determine scope and severity
      ↓
Follow incident-response procedures
      ↓
Document findings
```

---

# Important SOC Mindset

A SIEM alert is a **starting point for investigation**, not automatically proof of compromise.

A good SOC analyst asks:

```text
What triggered the alert?
What evidence supports it?
Is the activity expected?
What other events happened around the same time?
Are other hosts or users involved?
What is the scope?
What is still unknown?
```

The goal is to move from:

```text
Alert
  ↓
Evidence
  ↓
Context
  ↓
Correlation
  ↓
Investigation
  ↓
Documented conclusion
```

> Always follow your organization's escalation, containment, and incident-response procedures.

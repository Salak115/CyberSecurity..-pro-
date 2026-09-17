# SOC Analyst Toolbox

A practical reference list of tools commonly used across Security Operations Centers (SOCs).

> **Important:** Tools used for security testing should only be used on systems you own, authorized lab environments, or systems where you have explicit permission to test.

---

## 1. SIEM — Security Information and Event Management

SIEM platforms collect, search, correlate, and analyze security logs and events.

| Tool | Main function |
|---|---|
| **Splunk Enterprise Security** | Log analysis, correlation, alert investigation, and security monitoring |
| **Microsoft Sentinel** | Cloud SIEM, security analytics, detection, and investigation |
| **IBM QRadar** | Security-event collection, correlation, and investigation |
| **Elastic Security** | Search, detection, threat hunting, and security analytics |
| **Wazuh** | Open-source security monitoring, detection, and endpoint visibility |
| **Graylog** | Centralized log management and alerting |
| **LogRhythm** | SIEM and security monitoring |
| **Rapid7 InsightIDR** | SIEM, detection, and investigation |
| **FortiSIEM** | SIEM and security-event monitoring |
| **ManageEngine Log360** | Log management and security monitoring |

---

## 2. EDR / XDR — Endpoint Detection and Response

These tools provide visibility into computers, processes, files, network connections, and endpoint threats.

| Tool | Main function |
|---|---|
| **CrowdStrike Falcon** | Endpoint detection, investigation, and response |
| **Microsoft Defender for Endpoint** | Endpoint protection, detection, and investigation |
| **SentinelOne Singularity** | Endpoint detection and automated response |
| **VMware Carbon Black** | Endpoint visibility and threat detection |
| **Sophos Intercept X** | Endpoint protection and response |
| **Trend Micro Vision One** | XDR and threat investigation |
| **Cybereason** | Endpoint detection and investigation |
| **Trellix** | Endpoint security and security operations |
| **LimaCharlie** | Cloud-based endpoint telemetry and response |
| **OSQuery** | Query endpoint information using SQL-like queries |

---

## 3. Network Monitoring & Detection

These tools help analysts understand network traffic and identify suspicious activity.

| Tool | Main function |
|---|---|
| **Wireshark** | Capture and inspect individual network packets |
| **Zeek** | Generate detailed network-security logs |
| **Suricata** | Network IDS/IPS and traffic detection |
| **Snort** | Network intrusion detection and prevention |
| **tcpdump** | Capture network traffic from the command line |
| **Arkime** | Large-scale network traffic analysis |
| **Security Onion** | Platform combining network-security monitoring tools |
| **ExtraHop** | Network detection and response |
| **Darktrace** | Network behavior and anomaly detection |

---

## 4. Threat Intelligence

Threat-intelligence tools help investigate indicators such as IP addresses, domains, URLs, files, and hashes.

| Tool | Main function |
|---|---|
| **VirusTotal** | Investigate files, URLs, domains, and IP addresses |
| **MISP** | Manage and share threat intelligence |
| **AlienVault OTX** | Community threat intelligence |
| **AbuseIPDB** | Investigate suspicious IP addresses |
| **ThreatConnect** | Threat-intelligence management |
| **Recorded Future** | Commercial threat intelligence |
| **Anomali** | Threat intelligence and IOC management |
| **OpenCTI** | Organize and correlate threat intelligence |
| **GreyNoise** | Understand internet scanning and background noise |
| **URLhaus** | Research malicious URLs |
| **MalwareBazaar** | Malware sample intelligence |
| **Shodan** | Research internet-exposed services and devices |

---

## 5. Detection Engineering

Detection engineering focuses on creating and improving rules that identify suspicious behavior.

| Tool / Technology | Main function |
|---|---|
| **Sigma** | Portable detection rules for security logs |
| **YARA** | Pattern-based detection of files and malware |
| **Suricata Rules** | Network detection signatures |
| **Snort Rules** | Network intrusion detection rules |
| **MITRE ATT&CK** | Map observed activity to attacker techniques |
| **Atomic Red Team** | Safely emulate ATT&CK techniques in authorized environments |
| **KQL** | Query language widely used with Microsoft security products |
| **SPL** | Splunk Search Processing Language |
| **EQL** | Event Query Language used in Elastic environments |

---

## 6. SOAR — Security Orchestration, Automation and Response

SOAR tools connect security products and automate repeatable workflows.

| Tool | Main function |
|---|---|
| **Cortex XSOAR** | Security orchestration and automated response |
| **Splunk SOAR** | Automate investigations and response |
| **Tines** | Security workflow automation |
| **Swimlane** | SOAR and security automation |
| **Torq** | Security workflow automation |
| **FortiSOAR** | Security orchestration |
| **IBM QRadar SOAR** | Incident-response orchestration |

### Example SOC workflow

```text
SIEM detects suspicious IP
        ↓
SOAR receives alert
        ↓
Threat-intelligence lookup
        ↓
Create/update incident
        ↓
Notify analyst
        ↓
Analyst investigates
```

---

## 7. Incident Response & Case Management

These tools help organize investigations, evidence, tasks, and incident records.

| Tool | Main function |
|---|---|
| **TheHive** | Manage security investigations and cases |
| **ServiceNow** | Enterprise incident and case management |
| **Jira** | Track security incidents and tasks |
| **DFIR-IRIS** | Open-source incident-response management |
| **Cortex** | Analyze observables and support investigation workflows |

---

## 8. Digital Forensics

Forensics tools help determine what happened during a security incident.

| Tool | Main function |
|---|---|
| **Autopsy** | Digital forensic investigation |
| **FTK** | Digital forensics and evidence analysis |
| **EnCase** | Digital investigation and forensics |
| **Volatility** | Memory-dump analysis |
| **Velociraptor** | Endpoint collection and investigation |
| **KAPE** | Rapid forensic artifact collection |
| **Plaso** | Build forensic timelines |
| **Eric Zimmerman Tools** | Windows forensic analysis |

---

## 9. Windows Security Investigation

Windows knowledge is especially important for SOC analysts.

| Tool | Main function |
|---|---|
| **Sysmon** | Generate detailed Windows security telemetry |
| **Event Viewer** | Examine Windows event logs |
| **PowerShell** | Investigate and automate Windows systems |
| **Microsoft Defender** | Endpoint protection and investigation |
| **Autoruns** | Examine programs configured to start automatically |
| **Process Explorer** | Investigate running processes |
| **Process Monitor** | Monitor files, registry, processes, and system activity |
| **OSQuery** | Query endpoint information |

---

## 10. Malware Analysis

These tools help analysts examine suspicious files and programs.

| Tool | Main function |
|---|---|
| **Ghidra** | Reverse engineer compiled programs |
| **IDA Pro** | Advanced reverse engineering |
| **x64dbg** | Windows debugging |
| **GDB** | Program debugging |
| **CAPE Sandbox** | Automated malware analysis |
| **Cuckoo Sandbox** | Execute and analyze suspicious files in a sandbox |
| **YARA** | Detect malware patterns |
| **Detect It Easy (DIE)** | Identify executable characteristics |
| **PEStudio** | Analyze Windows executables |

---

## 11. Vulnerability Management

These tools help identify vulnerabilities in systems and software.

| Tool | Main function |
|---|---|
| **Nessus** | Vulnerability scanning |
| **OpenVAS / Greenbone** | Vulnerability assessment |
| **Qualys** | Enterprise vulnerability management |
| **Rapid7 InsightVM** | Vulnerability management |
| **Nmap** | Service and port discovery |
| **Trivy** | Container and dependency vulnerability scanning |

---

## 12. Identity & Active Directory

These tools help security teams understand identity systems and Active Directory environments.

| Tool | Main function |
|---|---|
| **BloodHound** | Map Active Directory relationships and attack paths |
| **PingCastle** | Assess Active Directory security |
| **Microsoft Entra ID** | Cloud identity management and monitoring |
| **AD Explorer** | Explore Active Directory |
| **PowerView** | Active Directory security assessment |

---

## 13. Email & Phishing Investigation

| Tool | Main function |
|---|---|
| **Microsoft Defender for Office 365** | Email threat detection and investigation |
| **Proofpoint** | Email security and phishing protection |
| **Mimecast** | Email security |
| **urlscan.io** | Analyze websites and URLs |
| **VirusTotal** | Investigate suspicious URLs and files |
| **PhishTool** | Analyze phishing emails |

---

# Recommended SOC Learning Roadmap

Do not try to master every tool at once.

## Phase 1 — Foundations

- Linux
- Networking
- Windows
- Python
- Git/GitHub

## Phase 2 — Network Visibility

- Wireshark
- Nmap
- tcpdump
- Zeek

## Phase 3 — SOC Core

- Wazuh
- Splunk
- Microsoft Sentinel
- Elastic Security

## Phase 4 — Endpoint Security

- Sysmon
- Microsoft Defender
- OSQuery
- Velociraptor

## Phase 5 — Threat Intelligence

- VirusTotal
- AbuseIPDB
- MISP
- MITRE ATT&CK

## Phase 6 — Detection Engineering

- Sigma
- YARA
- Suricata
- KQL
- SPL

## Phase 7 — Incident Response

- TheHive
- DFIR-IRIS
- SOAR concepts
- Incident-response methodology

## Phase 8 — Advanced Skills

- Threat hunting
- Digital forensics
- Malware analysis
- Detection engineering
- Security automation

---

# My Current Cybersecurity Experience

Tools and technologies I have already practiced:

- **Semgrep** — SAST
- **OWASP ZAP** — DAST
- **AFL++** — Fuzzing
- **Z3** — Constraint solving / symbolic-execution practice
- **Python** — Automation and machine learning
- **Docker** — Security lab environments
- **Git/GitHub** — Version control and documentation

---

# How I Will Document Each Tool

For every tool I learn, I will record:

1. **Tool name**
2. **Purpose**
3. **What problem it solves**
4. **Input**
5. **Important commands**
6. **Output and how to interpret it**
7. **SOC/security use**
8. **Practice lab**
9. **What I learned**
10. **Mistakes and how I fixed them**
11. **Screenshots/evidence**
12. **Related tools**

---

# Key SOC Mindset

A SOC analyst should not focus only on operating tools.

The goal is to understand the investigation process:

```text
ALERT
  ↓
TRIAGE
  ↓
COLLECT EVIDENCE
  ↓
INVESTIGATE
  ↓
DETERMINE WHAT HAPPENED
  ↓
CONTAIN / ESCALATE
  ↓
DOCUMENT
  ↓
IMPROVE DETECTION
```

The most important skill is connecting information from different sources.

For example:

```text
SIEM Alert
    +
Windows Event Logs
    +
EDR Telemetry
    +
Network Traffic
    +
Threat Intelligence
    ↓
SOC Analyst
    ↓
Incident Investigation
```

This toolbox will grow as I continue learning cybersecurity.

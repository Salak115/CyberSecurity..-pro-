# SOC Investigation Commands — SOC Analyst

A practical command reference for investigating security alerts and incidents.

> Use these commands only on systems, accounts, and network traffic you are authorized to investigate.

## 1. Alert Investigation

When a SOC alert appears, first collect the basic facts.

Ask:

- What happened?
- When did it happen?
- Which computer is affected?
- Which user is involved?
- What IP address or domain is involved?
- What process or file is involved?
- What evidence supports the alert?

Useful commands from the other toolbox sections include:

```text
hostname
whoami
ipconfig /all
netstat -ano
tasklist
Get-WinEvent
```

**SOC use:** Establish the basic context before deciding what the alert means.

---

## 2. IP Address Investigation

### Linux/macOS

```bash
ping <IP>
```

**SOC use:** Perform a basic connectivity check.

```bash
traceroute <IP>
```

**SOC use:** Examine the network path to a destination.

```bash
arp -a
```

**SOC use:** Review local IP-to-MAC mappings.

### Windows

```cmd
ping <IP>
tracert <IP>
arp -a
```

**SOC use:** Perform basic connectivity and local network checks.

> A failed ping does not prove that a host is offline. ICMP may be blocked.

---

## 3. Domain and DNS Investigation

### `nslookup`

```bash
nslookup suspicious-domain.com
```

Windows:

```cmd
nslookup suspicious-domain.com
```

**SOC use:** Determine which IP address a domain resolves to.

### `dig`

```bash
dig suspicious-domain.com
```

**SOC use:** Examine DNS information in more detail.

### Wireshark

Use:

```text
dns
```

To investigate a specific DNS query:

```text
dns.qry.name == "suspicious-domain.com"
```

**SOC use:** Investigate domains requested by a host in captured network traffic.

---

## 4. User and Login Investigation

### Linux

```bash
who
```

Shows currently logged-in users.

```bash
w
```

Shows active sessions and activity.

```bash
last
```

Shows login history.

```bash
id <username>
```

Shows user and group information.

**SOC use:** Investigate unexpected accounts, sessions, and login activity.

### Windows

```cmd
whoami
net user
net user <username>
net localgroup administrators
```

**SOC use:** Investigate the current account, local users, and administrator privileges.

---

## 5. Process Investigation

Processes are programs currently running on a system.

### Linux

```bash
ps aux
```

**SOC use:** Review running processes.

```bash
top
```

**SOC use:** Monitor processes and resource usage.

```bash
pgrep <process>
```

**SOC use:** Check whether a specific process is running.

### Windows

```cmd
tasklist
```

**SOC use:** Review running processes.

```cmd
tasklist /fi "imagename eq powershell.exe"
```

**SOC use:** Check for a specific process.

### PowerShell

```powershell
Get-Process
```

**SOC use:** Review running Windows processes.

```powershell
Get-Process | Select-Object Name, Id, Path
```

**SOC use:** Connect a process name and PID to its executable path.

---

## 6. Network Connection Investigation

### Linux

```bash
ss -tuln
```

Shows listening TCP/UDP sockets.

```bash
lsof -i
```

Shows processes using network connections.

### Windows

```cmd
netstat -ano
```

Shows connections, listening ports, and PIDs.

### PowerShell

```powershell
Get-NetTCPConnection
```

Shows TCP connections.

```powershell
Get-NetTCPConnection -State Established
```

Shows established TCP connections.

```powershell
Get-NetTCPConnection -State Listen
```

Shows listening TCP ports.

**SOC use:** Identify unusual connections and connect network activity to processes.

---

## 7. File Investigation

### Linux/macOS

```bash
ls -la
```

**SOC use:** Look for hidden or unusual files.

```bash
file suspicious_file
```

**SOC use:** Identify the type of a file.

```bash
stat suspicious_file
```

**SOC use:** Examine file metadata and timestamps.

```bash
find /tmp -type f
```

**SOC use:** Search for files in a location that may contain temporary or suspicious files.

### Windows

```cmd
dir /a
```

**SOC use:** List files, including hidden/system entries.

```cmd
where suspicious.exe
```

**SOC use:** Find an executable's location.

### PowerShell

```powershell
Get-ChildItem
```

**SOC use:** List files and directories.

---

## 8. File Hash Investigation

A file hash is a value calculated from file contents.

### PowerShell

```powershell
Get-FileHash suspicious.exe -Algorithm SHA256
```

### Linux

```bash
sha256sum suspicious_file
```

**SOC use:** Generate a SHA-256 hash that can be compared with known indicators or threat-intelligence records.

Example:

```text
SHA-256:
<hash value>
```

**Important:** A hash is an identifier for the file contents. It does not by itself prove that a file is malicious.

---

## 9. Log Investigation

Logs provide evidence about what happened on a system.

### Linux

Check available logs:

```bash
ls /var/log
```

Search for a keyword:

```bash
grep -i "failed" /var/log/auth.log
```

View recent lines:

```bash
tail /var/log/auth.log
```

**SOC use:** Investigate authentication and system activity.

### Linux with systemd

```bash
journalctl
```

Recent warnings:

```bash
journalctl -p warning
```

**SOC use:** Investigate system events.

> Log locations and filenames vary between Linux distributions.

### Windows

List Event Logs:

```cmd
wevtutil el
```

Query recent Security events:

```cmd
wevtutil qe Security /c:10 /rd:true /f:text
```

PowerShell:

```powershell
Get-WinEvent -LogName Security -MaxEvents 10
```

**SOC use:** Investigate Windows security events.

### Failed Windows logons

```powershell
Get-WinEvent -FilterHashtable @{LogName='Security'; Id=4625} -MaxEvents 20
```

Event ID `4625` represents a failed logon event.

**SOC use:** Investigate failed authentication attempts.

---

## 10. File Permissions

### Linux

```bash
ls -l suspicious_file
```

**SOC use:** Review file permissions and ownership.

```bash
id <username>
```

**SOC use:** Understand the user's groups and privileges.

### Windows

```cmd
icacls suspicious.exe
```

**SOC use:** Review Windows file and directory permissions.

---

## 11. Suspicious Command Investigation

### PowerShell history

```powershell
Get-History
```

**SOC use:** Review commands entered during the current PowerShell session.

### Linux shell history

```bash
history
```

**SOC use:** Review commands from the current shell history.

> Command history is not a complete record of everything executed. History settings and logging vary between systems.

---

## 12. Timeline Building

A SOC analyst should establish a timeline.

Record:

```text
Time
↓
User
↓
Host
↓
Process
↓
File
↓
IP/domain
↓
Network connection
↓
Log event
```

Useful evidence sources include:

```text
Windows Event Logs
Linux logs
Process information
Network connections
PCAP files
File timestamps
Authentication events
SIEM alerts
```

**SOC use:** A timeline helps connect separate events into one investigation.

---

## 13. Basic Incident Response

When an alert appears:

### Step 1 — Identify

Determine:

```text
Host
User
Time
IP/domain
Process
File
Alert type
```

### Step 2 — Validate

Ask:

```text
Is the activity expected?
Is the account legitimate?
Is the process legitimate?
Is the destination expected?
Is there supporting evidence?
```

### Step 3 — Scope

Determine whether other:

```text
Users
Hosts
Processes
Files
IPs
Domains
```

are involved.

### Step 4 — Contain

If malicious activity is confirmed, follow the organization's approved incident-response procedures.

Possible authorized actions can include:

```text
Isolating a host
Disabling a compromised account
Blocking a malicious indicator
Stopping a confirmed malicious process
```

### Step 5 — Eradicate and Recover

Remove the confirmed cause according to organizational procedures and restore affected systems safely.

### Step 6 — Document

Record:

```text
What happened
When it happened
What evidence was found
What systems were affected
What actions were taken
What remains uncertain
```

---

# Quick SOC Investigation Reference

| Investigation question | Useful command/tool |
|---|---|
| What host am I investigating? | `hostname` |
| Which user am I? | `whoami` |
| Who is logged in? | `who`, `w` |
| What users exist? | `net user` |
| What is the login history? | `last` |
| What is the network configuration? | `ipconfig /all` |
| What connections exist? | `netstat -ano` |
| What processes are running? | `tasklist` / `ps aux` |
| What process owns a connection? | `netstat -ano` + PID / `lsof -i` |
| What ports are listening? | `ss -tuln` |
| What domain does an IP/domain resolve to? | `nslookup` / `dig` |
| What files are present? | `ls -la` / `dir /a` |
| What type is a suspicious file? | `file` |
| What are file timestamps? | `stat` |
| What is the file hash? | `sha256sum` / `Get-FileHash` |
| What permissions does a file have? | `ls -l` / `icacls` |
| What happened in Linux logs? | `grep` / `journalctl` |
| What happened in Windows logs? | `Get-WinEvent` / `wevtutil` |
| What failed Windows logons exist? | Security Event ID `4625` |
| What DNS traffic exists in a PCAP? | Wireshark `dns` |
| What traffic involves an IP? | Wireshark `ip.addr == <IP>` |

---

# SOC Investigation Flow

```text
🚨 SOC Alert
      ↓
Identify host + user + time
      ↓
Identify IP / domain / process / file
      ↓
Check logs
      ↓
Check authentication activity
      ↓
Check running processes
      ↓
Check network connections
      ↓
Check suspicious files
      ↓
Calculate file hash
      ↓
Correlate all evidence
      ↓
Determine scope
      ↓
Follow incident-response procedures
      ↓
Document findings
```

---

# SOC Analyst Mindset

Do not investigate an alert using only one piece of evidence.

Try to correlate:

```text
SIEM Alert
     +
Endpoint Evidence
     +
Network Evidence
     +
Authentication Evidence
     +
File Evidence
     +
Threat Intelligence
```

The goal is to understand:

```text
What happened?
Who was involved?
Which system was affected?
When did it happen?
How did it happen?
What evidence supports the conclusion?
What is still unknown?
```

> A suspicious indicator is not automatically malicious. Validate it using multiple sources of evidence and the context of the environment.

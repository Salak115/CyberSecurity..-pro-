# Windows Commands — SOC Analyst

A practical Windows command reference for SOC Analyst learning.

> These commands are intended for systems you own or are authorized to investigate.

## 1. System Information

### `hostname`
Shows the computer name.

```cmd
hostname
```

**SOC use:** Identify the Windows system being investigated.

### `systeminfo`
Displays detailed Windows system information.

```cmd
systeminfo
```

**SOC use:** Collect basic operating system, patch, and system information during an investigation.

### `whoami`
Shows the current user.

```cmd
whoami
```

**SOC use:** Identify which account is being used.

Useful:

```cmd
whoami /groups
whoami /priv
```

**SOC use:** Review the user's group memberships and privileges.

---

## 2. Network Investigation

### `ipconfig`
Displays Windows network configuration.

```cmd
ipconfig
```

More detailed:

```cmd
ipconfig /all
```

**SOC use:** Identify IP addresses, DNS servers, gateways, and network adapters.

### `ping`
Tests basic network connectivity.

```cmd
ping 8.8.8.8
```

**SOC use:** Perform basic connectivity checks.

**Important:** A failed ping does not necessarily mean the host is offline. ICMP may be blocked.

### `arp`
Displays the ARP cache.

```cmd
arp -a
```

**SOC use:** Investigate local IP-to-MAC address relationships.

### `netstat`
Displays network connections and listening ports.

```cmd
netstat -ano
```

`-a` shows connections and listening ports.

`-n` shows addresses numerically.

`-o` shows the process ID (PID).

**SOC use:** Find suspicious network connections and identify the process associated with a connection.

### `nslookup`
Queries DNS.

```cmd
nslookup example.com
```

**SOC use:** Investigate which IP address a domain resolves to.

---

## 3. Process Investigation

### `tasklist`
Displays running processes.

```cmd
tasklist
```

Detailed:

```cmd
tasklist /v
```

**SOC use:** Look for unexpected or suspicious processes.

### `tasklist` with a specific process

```cmd
tasklist /fi "imagename eq powershell.exe"
```

**SOC use:** Check whether a particular process is running.

### `taskkill`
Terminates a process.

```cmd
taskkill /PID <PID>
```

Force termination:

```cmd
taskkill /PID <PID> /F
```

**SOC use:** During authorized incident response, a confirmed malicious process may need to be stopped.

> Do not terminate a process unless you understand it and are authorized to do so.

---

## 4. Users and Accounts

### `net user`
Lists local user accounts.

```cmd
net user
```

**SOC use:** Investigate local accounts and identify unexpected accounts.

### `net user <username>`
Displays information about a specific user.

```cmd
net user username
```

**SOC use:** Review account status, groups, and other account information.

### `net localgroup`
Lists local groups.

```cmd
net localgroup
```

**SOC use:** Identify available local security groups.

### `net localgroup administrators`
Shows members of the local Administrators group.

```cmd
net localgroup administrators
```

**SOC use:** Investigate which accounts have local administrator privileges.

---

## 5. Windows Services

### `sc query`
Lists Windows services and their states.

```cmd
sc query
```

**SOC use:** Investigate running and stopped services.

### `sc query <service>`
Checks a specific service.

```cmd
sc query wuauserv
```

**SOC use:** Investigate whether a specific Windows service is running.

### PowerShell `Get-Service`

```powershell
Get-Service
```

**SOC use:** Review Windows services using PowerShell.

---

## 6. Windows Event Logs

Windows records security and system events in Event Logs.

Important logs include:

```text
Security
System
Application
```

### `wevtutil`
Windows command-line Event Log utility.

List logs:

```cmd
wevtutil el
```

**SOC use:** See which Windows event logs are available.

### Query a log

```cmd
wevtutil qe Security /c:10 /rd:true /f:text
```

This requests the latest 10 events from the Security log.

**SOC use:** Investigate authentication and security events.

### PowerShell `Get-WinEvent`

List recent Security events:

```powershell
Get-WinEvent -LogName Security -MaxEvents 10
```

**SOC use:** Investigate Windows security events.

### Filter Security events

Example:

```powershell
Get-WinEvent -FilterHashtable @{LogName='Security'; Id=4625} -MaxEvents 20
```

Event ID `4625` represents a failed logon event on Windows.

**SOC use:** Investigate failed authentication attempts.

---

## 7. PowerShell Process Investigation

### `Get-Process`

Lists running processes.

```powershell
Get-Process
```

**SOC use:** Investigate running processes.

### Find a process

```powershell
Get-Process powershell
```

**SOC use:** Check whether PowerShell is running.

### Process information

```powershell
Get-Process | Select-Object Name, Id, Path
```

**SOC use:** Connect a process name and PID with its executable path.

---

## 8. PowerShell Network Investigation

### `Get-NetTCPConnection`

Displays TCP connections.

```powershell
Get-NetTCPConnection
```

**SOC use:** Investigate active network connections.

### Show listening ports

```powershell
Get-NetTCPConnection -State Listen
```

**SOC use:** Identify services listening for incoming connections.

### Show established connections

```powershell
Get-NetTCPConnection -State Established
```

**SOC use:** Investigate active network sessions.

---

## 9. File Investigation

### `dir`
Lists files and directories.

```cmd
dir
```

Hidden/system items:

```cmd
dir /a
```

**SOC use:** Inspect directories and look for unusual files.

### `where`
Finds the location of an executable.

```cmd
where powershell
```

**SOC use:** Identify where an executable is located.

### PowerShell `Get-ChildItem`

```powershell
Get-ChildItem
```

Recursive search:

```powershell
Get-ChildItem -Recurse
```

**SOC use:** Investigate files and directories.

### `Get-FileHash`

Calculates a file hash.

```powershell
Get-FileHash suspicious.exe
```

SHA-256:

```powershell
Get-FileHash suspicious.exe -Algorithm SHA256
```

**SOC use:** Generate a file hash that can be compared with known malware indicators or threat-intelligence data.

---

## 10. File Permissions

### `icacls`
Displays Windows file and directory permissions.

```cmd
icacls suspicious.exe
```

**SOC use:** Investigate who can access or modify a suspicious file.

---

## 11. Environment and Command History

### `set`
Displays environment variables in Command Prompt.

```cmd
set
```

**SOC use:** Review environment information during an investigation.

### PowerShell history

```powershell
Get-History
```

**SOC use:** Review commands entered during the current PowerShell session.

> PowerShell history availability and persistence depend on the user's configuration.

---

# Quick SOC Analyst Reference

| Question | Command |
|---|---|
| What computer am I investigating? | `hostname` |
| What Windows version/system information exists? | `systeminfo` |
| Who am I? | `whoami` |
| What is the network configuration? | `ipconfig /all` |
| What IP/MAC mappings are known? | `arp -a` |
| What network connections exist? | `netstat -ano` |
| What domain/IP does DNS resolve to? | `nslookup <domain>` |
| What processes are running? | `tasklist` |
| Is a specific process running? | `tasklist /fi "imagename eq <name>"` |
| What local users exist? | `net user` |
| Who are local administrators? | `net localgroup administrators` |
| What services exist? | `sc query` |
| What event logs exist? | `wevtutil el` |
| Read recent Security events | `wevtutil qe Security /c:10 /rd:true /f:text` |
| Read recent Security events in PowerShell | `Get-WinEvent -LogName Security -MaxEvents 10` |
| Investigate failed logons | `Get-WinEvent -FilterHashtable @{LogName='Security'; Id=4625}` |
| What processes are running in PowerShell? | `Get-Process` |
| What TCP connections exist? | `Get-NetTCPConnection` |
| What ports are listening? | `Get-NetTCPConnection -State Listen` |
| Find an executable | `where <program>` |
| Calculate a file hash | `Get-FileHash <file> -Algorithm SHA256` |
| Check file permissions | `icacls <file>` |

---

# SOC Investigation Flow

```text
Suspicious Windows activity
        ↓
hostname / systeminfo
        ↓
Which Windows system is involved?
        ↓
whoami / net user
        ↓
Which account is involved?
        ↓
Get-WinEvent / wevtutil
        ↓
What happened in the Windows logs?
        ↓
tasklist / Get-Process
        ↓
Which processes are running?
        ↓
netstat -ano / Get-NetTCPConnection
        ↓
What network connections exist?
        ↓
Get-FileHash
        ↓
What is the file's hash?
        ↓
icacls
        ↓
Who can access or modify the file?
```

> Use these commands only on systems you own or are authorized to investigate.

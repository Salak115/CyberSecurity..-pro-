# Linux Commands — SOC Analyst

A practical Linux command reference for SOC Analyst learning.

## 1. Navigation and Files

### `pwd`
Shows the current directory.

```bash
pwd
```

**SOC use:** Know which directory you are currently investigating.

### `ls`
Lists files and directories.

```bash
ls
```

Useful:

```bash
ls -la
```

**SOC use:** Look for hidden files and suspicious files.

### `cd`
Moves to another directory.

```bash
cd /var/log
```

**SOC use:** Move into directories containing logs or investigation files.

### `mkdir`
Creates a directory.

```bash
mkdir investigation
```

**SOC use:** Create a folder to organize investigation evidence or notes.

### `touch`
Creates an empty file.

```bash
touch notes.txt
```

**SOC use:** Create investigation notes or evidence-tracking files.

### `cp`
Copies a file or directory.

```bash
cp suspicious.log investigation/
```

**SOC use:** Make a working copy of a file before analysis.

### `mv`
Moves or renames a file.

```bash
mv report.txt investigation/
```

**SOC use:** Organize investigation files.

### `rm`
Removes a file.

```bash
rm test.txt
```

**SOC use:** Remove temporary investigation files.

> Be careful with `rm`. Deleted files may not be recoverable.

---

## 2. Reading and Searching Files

### `cat`
Displays file contents.

```bash
cat notes.txt
```

**SOC use:** Quickly inspect small files and logs.

### `less`
Reads large files one page at a time.

```bash
less /var/log/system.log
```

**SOC use:** Investigate large log files without loading the entire file at once.

### `head`
Shows the beginning of a file.

```bash
head suspicious.log
```

**SOC use:** Quickly inspect the first entries in a log.

### `tail`
Shows the end of a file.

```bash
tail suspicious.log
```

To continuously watch new lines:

```bash
tail -f suspicious.log
```

**SOC use:** Monitor logs for new events.

### `grep`
Searches for text inside files.

```bash
grep "failed" suspicious.log
```

**SOC use:** Search logs for keywords such as failed logins, errors, usernames, or IP addresses.

Useful:

```bash
grep -i "failed" suspicious.log
grep -n "error" suspicious.log
```

`-i` ignores letter case.

`-n` shows line numbers.

### `find`
Searches for files and directories.

```bash
find /tmp -type f
```

**SOC use:** Find suspicious or recently created files.

Example:

```bash
find /tmp -type f -name "*.sh"
```

### `file`
Identifies the type of a file.

```bash
file suspicious_file
```

**SOC use:** Check whether a file is actually a script, executable, archive, text file, etc.

### `stat`
Displays detailed file metadata.

```bash
stat suspicious_file
```

**SOC use:** Examine file size, permissions, ownership, and timestamps.

---

## 3. Processes

### `ps`
Displays running processes.

```bash
ps
```

A more detailed view:

```bash
ps aux
```

**SOC use:** Look for suspicious or unexpected processes.

### `top`
Shows processes and system activity in real time.

```bash
top
```

**SOC use:** Investigate processes using unusual CPU or memory.

Press `q` to quit.

### `pgrep`
Finds processes by name.

```bash
pgrep ssh
```

**SOC use:** Quickly check whether a particular process is running.

### `kill`
Sends a signal to a process.

```bash
kill <PID>
```

**SOC use:** Can be used during an authorized incident response to stop a malicious or compromised process.

> Do not kill processes unless you understand what they are and are authorized to do so.

---

## 4. Users and Login Investigation

### `who`
Shows users currently logged in.

```bash
who
```

**SOC use:** Investigate unexpected active sessions.

### `w`
Shows logged-in users and what they are doing.

```bash
w
```

**SOC use:** Investigate active sessions and user activity.

### `id`
Shows user and group information.

```bash
id
```

For another user:

```bash
id username
```

**SOC use:** Check user identity and group privileges.

### `last`
Shows login history.

```bash
last
```

**SOC use:** Investigate unusual or unexpected logins.

### `lastlog`
Shows the most recent login for users.

```bash
lastlog
```

**SOC use:** Review account login activity.

---

## 5. Permissions and Ownership

### `ls -l`
Shows file permissions and ownership.

```bash
ls -l
```

Example:

```text
-rwxr-xr--  user  staff  suspicious.sh
```

**SOC use:** Investigate who owns a file and what permissions it has.

### `chmod`
Changes file permissions.

```bash
chmod 644 file.txt
```

**SOC use:** Understand and, when authorized, correct insecure permissions.

### `chown`
Changes file ownership.

```bash
chown user file.txt
```

**SOC use:** Understand or correct file ownership during authorized administration.

> Permission changes should only be made when authorized.

---

## 6. System Information

### `uname`
Shows system information.

```bash
uname -a
```

**SOC use:** Identify the operating system and kernel information during an investigation.

### `hostname`
Shows the system hostname.

```bash
hostname
```

**SOC use:** Identify which machine you are investigating.

### `uptime`
Shows how long the system has been running.

```bash
uptime
```

**SOC use:** Help establish basic system activity context.

### `df`
Shows available disk space.

```bash
df -h
```

**SOC use:** Investigate unusual disk usage or storage problems.

### `du`
Shows directory and file sizes.

```bash
du -sh *
```

**SOC use:** Find directories using an unusual amount of disk space.

---

## 7. Logs

Linux systems commonly store security and system information in log files.

Common locations include:

```text
/var/log/
```

### `ls /var/log`
Lists available log files.

```bash
ls /var/log
```

**SOC use:** Identify logs available for investigation.

### `journalctl`
Displays logs collected by systemd-based systems.

```bash
journalctl
```

Useful:

```bash
journalctl -b
journalctl -p warning
```

**SOC use:** Investigate system events and warnings.

> macOS does not use systemd, so `journalctl` is mainly useful when investigating Linux systems.

### `grep` + logs

Example:

```bash
grep -i "failed" /var/log/auth.log
```

**SOC use:** Search authentication logs for failed login attempts.

> Log filenames and locations vary between Linux distributions.

---

## 8. Network Investigation

### `ss`
Displays network sockets and connections on Linux.

```bash
ss
```

Useful:

```bash
ss -tuln
```

**SOC use:** Investigate listening ports and network connections.

### `lsof`
Shows files and resources opened by processes.

```bash
lsof
```

For network connections:

```bash
lsof -i
```

**SOC use:** Connect a network connection to the process using it.

### `curl`
Makes HTTP/HTTPS requests.

```bash
curl -I https://example.com
```

**SOC use:** Inspect HTTP response headers and investigate web communication.

### `ping`
Tests basic network reachability.

```bash
ping 8.8.8.8
```

**SOC use:** Perform basic connectivity checks during an investigation.

---

# Quick SOC Analyst Reference

| Question | Command |
|---|---|
| Where am I? | `pwd` |
| What files are here? | `ls -la` |
| Read a file | `cat <file>` |
| Read a large file | `less <file>` |
| See the latest log entries | `tail <file>` |
| Watch new log entries | `tail -f <file>` |
| Search a log | `grep "keyword" <file>` |
| Find files | `find <path> -type f` |
| Identify a file | `file <file>` |
| Check file metadata | `stat <file>` |
| See running processes | `ps aux` |
| Monitor processes | `top` |
| Find a process | `pgrep <name>` |
| See logged-in users | `who` |
| See active user sessions | `w` |
| Check user information | `id <user>` |
| Check login history | `last` |
| Check file permissions | `ls -l` |
| Check system information | `uname -a` |
| Check hostname | `hostname` |
| Check disk space | `df -h` |
| Check directory size | `du -sh *` |
| Investigate Linux logs | `journalctl` |
| Check listening ports | `ss -tuln` |
| Find network processes | `lsof -i` |
| Inspect HTTP headers | `curl -I <URL>` |

---

# SOC Investigation Flow

```text
Suspicious Linux activity
        ↓
who / w / last
        ↓
Which user or account is involved?
        ↓
grep / journalctl
        ↓
What happened in the logs?
        ↓
ps aux / top
        ↓
Which processes are running?
        ↓
ss / lsof -i
        ↓
What network connections exist?
        ↓
find / stat / file
        ↓
Are there suspicious files?
        ↓
ls -l / id
        ↓
What permissions and privileges are involved?
```

> Use these commands only on systems you own or are authorized to investigate.

# Cybersecurity Toolbox — 50 Tools

A personal reference guide for learning cybersecurity tools and understanding what each tool is useful for.

> **Important:** Practice security testing only on systems you own or have explicit permission to test.

## 1. Reconnaissance & Network Security

| # | Tool | Usefulness |
|---|---|---|
| 1 | **Nmap** | Discover hosts, open ports, and running services. |
| 2 | **Masscan** | Perform very fast large-scale port scanning. |
| 3 | **Wireshark** | Capture and analyze network packets. |
| 4 | **tcpdump** | Capture and inspect network traffic from the terminal. |
| 5 | **Netcat (nc)** | Test network connections and transfer data. |
| 6 | **WHOIS** | Look up domain registration information. |
| 7 | **dig** | Query DNS records. |
| 8 | **nslookup** | Perform DNS lookups. |
| 9 | **Traceroute** | See the network path toward a host. |
| 10 | **Amass** | Discover and map domains and subdomains. |

## 2. Web Application Security

| # | Tool | Usefulness |
|---|---|---|
| 11 | **OWASP ZAP** | Perform DAST scans against running web applications. |
| 12 | **Burp Suite** | Inspect and modify HTTP requests and responses. |
| 13 | **ffuf** | Discover hidden directories and endpoints on authorized targets. |
| 14 | **Gobuster** | Perform directory, DNS, and virtual-host enumeration. |
| 15 | **Nikto** | Check web servers for known insecure configurations. |
| 16 | **SQLMap** | Test for SQL injection in authorized applications. |
| 17 | **Wapiti** | Scan web applications for common vulnerabilities. |
| 18 | **WhatWeb** | Identify technologies used by a website. |
| 19 | **httpx** | Probe HTTP services and collect information about them. |
| 20 | **Nuclei** | Perform template-based vulnerability and misconfiguration scanning. |

## 3. Source Code & Application Security

| # | Tool | Usefulness |
|---|---|---|
| 21 | **Semgrep** | SAST — find insecure coding patterns in source code. |
| 22 | **CodeQL** | Analyze source code for security vulnerabilities. |
| 23 | **SonarQube** | Analyze code quality and security issues. |
| 24 | **Bandit** | Find common security issues in Python code. |
| 25 | **Brakeman** | Perform security analysis of Ruby on Rails applications. |
| 26 | **ESLint** | Find problems and security-related issues in JavaScript/TypeScript code. |
| 27 | **Gitleaks** | Find accidentally exposed secrets in Git repositories. |
| 28 | **Trivy** | Scan containers, filesystems, and dependencies for vulnerabilities. |
| 29 | **Snyk** | Find vulnerabilities in dependencies and code. |
| 30 | **OWASP Dependency-Check** | Identify known vulnerable software dependencies. |

## 4. Fuzzing & Program Analysis

| # | Tool | Usefulness |
|---|---|---|
| 31 | **AFL++** | Fuzz programs to discover crashes and unexpected behavior. |
| 32 | **libFuzzer** | Perform in-process fuzzing of programs and libraries. |
| 33 | **Honggfuzz** | Perform coverage-guided fuzzing. |
| 34 | **Z3** | Solve mathematical and program constraints. |
| 35 | **angr** | Perform binary analysis and symbolic execution. |
| 36 | **Ghidra** | Reverse engineer compiled programs. |
| 37 | **GDB** | Debug and inspect program execution. |
| 38 | **Radare2** | Perform reverse engineering and binary analysis. |
| 39 | **Valgrind** | Detect memory errors and analyze program behavior. |
| 40 | **strace** | Observe system calls made by programs on Linux. |

## 5. Passwords, Forensics & Security Operations

| # | Tool | Usefulness |
|---|---|---|
| 41 | **Hashcat** | Audit password hashes in authorized environments. |
| 42 | **John the Ripper** | Perform password/hash security testing. |
| 43 | **Autopsy** | Perform digital forensics investigations. |
| 44 | **Volatility** | Analyze memory dumps. |
| 45 | **YARA** | Identify files or memory using pattern-based rules. |
| 46 | **ClamAV** | Detect known malware using antivirus signatures. |
| 47 | **Wazuh** | Perform security monitoring and threat detection. |
| 48 | **Splunk** | Search and analyze security logs. |
| 49 | **TheHive** | Organize and manage security incidents. |
| 50 | **MISP** | Manage and share threat-intelligence information. |

# Learning Roadmap

### Beginner
- Nmap
- Wireshark
- Linux
- Python
- Semgrep
- OWASP ZAP
- Git/GitHub
- Docker

### Intermediate
- Burp Suite
- ffuf
- Gitleaks
- Trivy
- Nuclei
- CodeQL
- AFL++
- Ghidra
- GDB

### Advanced
- angr
- YARA
- Volatility
- Wazuh
- MISP
- Splunk

# How I Will Document Each Tool

For every tool I learn, I will record:

1. **Tool name**
2. **Purpose** — What problem does it solve?
3. **Input** — What do I give the tool?
4. **Commands** — Important commands I learn.
5. **Output** — What does the output mean?
6. **Security use** — What can it help me discover?
7. **Practice lab** — Where can I safely practice?
8. **My notes** — What did I learn?
9. **My mistakes** — What went wrong and how did I fix it?

# Tools I Have Already Practiced

- **Semgrep** — SAST
- **OWASP ZAP** — DAST
- **AFL++** — Fuzzing
- **Z3** — Constraint solving / symbolic-execution practice
- **Python** — Automation and ML practice
- **Docker** — Running security practice environments
- **Git/GitHub** — Version control and project documentation

# Key Idea

Cybersecurity is not about memorizing 50 tools.

The goal is to understand:

**Problem → Security technique → Tool → Evidence → Analysis → Fix**

Examples:

**Source-code vulnerability → SAST → Semgrep → Finding → Investigate → Fix → Rescan**

**Running web application → DAST → OWASP ZAP → Alert → Investigate → Fix → Retest**

**Network visibility → Packet analysis → Wireshark → Packets → Investigate → Understand traffic**

This toolbox will grow as I learn more.

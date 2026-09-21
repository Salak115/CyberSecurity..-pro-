# Networking Commands — SOC Analyst

A practical networking command reference for SOC Analyst learning on macOS/Linux.

## 1. Network Information

### `ifconfig`
Displays network interfaces, IP addresses, MAC addresses, and interface status.

```bash
ifconfig
```

**SOC use:** Check network interfaces and identify IP/MAC information.

### `ifconfig en0`
Displays information specifically for the `en0` interface.

```bash
ifconfig en0
```

Look for:
- `inet` → IPv4 address
- `inet6` → IPv6 address
- `ether` → MAC address
- `status: active` → active interface

### `ipconfig getifaddr en0`
Quickly displays the IPv4 address assigned to `en0`.

```bash
ipconfig getifaddr en0
```

### `arp -a`
Displays the ARP table, showing IP-to-MAC mappings known by the computer.

```bash
arp -a
```

**SOC use:** Investigate devices known on the local network and their IP/MAC relationships.

### `netstat -rn`
Displays the routing table.

```bash
netstat -rn
```

**SOC use:** Understand how network traffic is routed.

### `route -n get default`
Shows information about the default route/gateway.

```bash
route -n get default
```

**SOC use:** Identify the gateway used for outbound traffic.

---

## 2. Connectivity and Network Path

### `ping`
Tests basic network reachability and measures response time.

```bash
ping 8.8.8.8
```

Stop a continuous ping with **Control + C**.

**SOC use:** Check whether a host responds and investigate basic connectivity.

**Important:** A failed ping does not necessarily mean a host is offline. Firewalls or network policies can block ICMP.

### `traceroute`
Shows the network hops between your computer and a destination.

```bash
traceroute 8.8.8.8
```

**SOC use:** Understand the path traffic takes and investigate routing problems.

---

## 3. DNS Investigation

### `nslookup`
Queries DNS information.

```bash
nslookup google.com
```

**SOC use:** Investigate which IP address a domain resolves to.

### `dig`
Performs detailed DNS queries.

```bash
dig google.com
```

Useful examples:

```bash
dig google.com A
dig google.com MX
dig google.com TXT
```

**SOC use:** Investigate DNS records and suspicious domains.

---

## 4. Network Connections and Ports

### `lsof -i`
Shows processes using network connections.

```bash
lsof -i
```

**SOC use:** Identify which applications/processes are communicating over the network.

### `lsof -iTCP -sTCP:LISTEN`
Shows TCP services listening for connections.

```bash
lsof -iTCP -sTCP:LISTEN
```

**SOC use:** Investigate services listening for incoming connections.

### `nc`
Netcat can test network connections and ports.

```bash
nc -vz 127.0.0.1 3000
```

**SOC use:** Test a specific TCP port during an authorized investigation.

---

## 5. Web / HTTP Investigation

### `curl -I`
Requests HTTP response headers.

```bash
curl -I https://example.com
```

**SOC use:** Inspect HTTP status codes and response headers.

### `curl -v`
Displays detailed information about an HTTP/HTTPS connection.

```bash
curl -v https://example.com
```

**SOC use:** Investigate web connections, redirects, headers, and TLS connection details.

---

# Quick SOC Analyst Reference

| Question | Command |
|---|---|
| What is my IP? | `ipconfig getifaddr en0` |
| What is my MAC? | `ifconfig en0` |
| What interfaces do I have? | `ifconfig` |
| What IP/MAC pairs do I know locally? | `arp -a` |
| Where does my traffic go? | `netstat -rn` |
| Who is my router? | `route -n get default` |
| Can I reach a host? | `ping <IP>` |
| What route does traffic take? | `traceroute <IP>` |
| What IP does a domain use? | `nslookup <domain>` / `dig <domain>` |
| What programs are using the network? | `lsof -i` |
| What TCP services are listening? | `lsof -iTCP -sTCP:LISTEN` |
| Is a port reachable? | `nc -vz <IP> <PORT>` |
| What HTTP headers does a site return? | `curl -I <URL>` |
| Show detailed web connection information | `curl -v <URL>` |

---

# SOC Investigation Flow

```text
Suspicious IP/domain
       ↓
nslookup / dig
       ↓
What does the domain resolve to?
       ↓
ping
       ↓
Does the host respond?
       ↓
traceroute
       ↓
What path does traffic take?
       ↓
lsof -i
       ↓
Which local process is communicating?
       ↓
arp -a
       ↓
Which local IP/MAC relationships are known?
       ↓
netstat -rn
       ↓
How is traffic being routed?
```

> Use these commands only on systems and networks you are authorized to investigate.

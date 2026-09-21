# Wireshark Cheat Sheet — SOC Analyst

A practical Wireshark reference for SOC Analyst learning and basic network traffic investigation.

> Use Wireshark only on traffic and systems you are authorized to monitor.

## 1. What is Wireshark?

Wireshark is a network protocol analyzer.

It allows an analyst to:

- Capture network traffic
- Inspect packets
- Filter traffic
- Investigate protocols
- Identify communicating IP addresses
- Investigate suspicious connections
- Analyze PCAP files

**SOC use:** Wireshark can help an analyst understand what happened during a network security investigation.

---

## 2. Starting a Capture

Open Wireshark and select the network interface that is carrying traffic.

Common interfaces can include:

```text
Wi-Fi
Ethernet
en0
```

Start the capture and generate normal network traffic, such as visiting a website.

Stop the capture when you have enough traffic to investigate.

**SOC use:** Capture traffic when authorized and use the packets as evidence for investigation.

---

## 3. Display Filters

Wireshark display filters help you focus on specific traffic.

### IP address

Show traffic involving an IP address:

```text
ip.addr == 10.2.8.194
```

**SOC use:** Investigate traffic involving a specific host.

### Source IP

```text
ip.src == 10.2.8.194
```

**SOC use:** Find packets sent from a specific IP.

### Destination IP

```text
ip.dst == 8.8.8.8
```

**SOC use:** Find traffic going to a specific destination.

### Multiple IP conditions

```text
ip.addr == 10.2.8.194 && ip.addr == 8.8.8.8
```

**SOC use:** Focus on communication between two hosts.

---

## 4. TCP Investigation

### Show TCP traffic

```text
tcp
```

**SOC use:** Focus on TCP communications.

### TCP port

```text
tcp.port == 443
```

**SOC use:** Investigate traffic using a specific TCP port.

### Source TCP port

```text
tcp.srcport == 443
```

### Destination TCP port

```text
tcp.dstport == 443
```

### TCP SYN packets

```text
tcp.flags.syn == 1
```

**SOC use:** Investigate connection attempts.

### SYN without ACK

```text
tcp.flags.syn == 1 && tcp.flags.ack == 0
```

**SOC use:** Investigate initial TCP connection attempts.

---

## 5. UDP Investigation

### Show UDP traffic

```text
udp
```

**SOC use:** Focus on UDP communications.

### UDP port

```text
udp.port == 53
```

**SOC use:** Investigate UDP traffic using a specific port, such as DNS.

---

## 6. DNS Investigation

### Show DNS traffic

```text
dns
```

**SOC use:** Investigate domain lookups.

### DNS queries

```text
dns.flags.response == 0
```

**SOC use:** Focus on DNS requests.

### DNS responses

```text
dns.flags.response == 1
```

**SOC use:** Focus on DNS responses.

### Find a domain

```text
dns.qry.name == "example.com"
```

**SOC use:** Investigate requests for a specific domain.

### DNS query name contains text

```text
dns.qry.name contains "example"
```

**SOC use:** Search for domains containing a particular string.

---

## 7. HTTP Investigation

### Show HTTP traffic

```text
http
```

**SOC use:** Investigate unencrypted HTTP traffic.

### HTTP requests

```text
http.request
```

**SOC use:** Focus on HTTP requests.

### HTTP response

```text
http.response
```

**SOC use:** Investigate HTTP server responses.

### HTTP host

```text
http.host
```

**SOC use:** Identify HTTP host information.

### HTTP method

```text
http.request.method == "GET"
```

**SOC use:** Investigate specific HTTP request methods.

> HTTP can expose information in plaintext. HTTPS encrypts application data, so you generally cannot inspect the protected HTTP contents directly without the appropriate decryption context.

---

## 8. TLS / HTTPS Investigation

### Show TLS traffic

```text
tls
```

**SOC use:** Focus on TLS-encrypted traffic.

### TLS handshake

```text
tls.handshake
```

**SOC use:** Investigate TLS connection setup.

### TLS Client Hello

```text
tls.handshake.type == 1
```

**SOC use:** Identify TLS Client Hello packets.

### TLS Server Name

Depending on the capture and TLS version, the Server Name Indication may be visible:

```text
tls.handshake.extensions_server_name
```

**SOC use:** Investigate the hostname presented during a TLS handshake.

> Modern encrypted protocols and TLS versions can limit what information is visible in a packet capture.

---

## 9. ICMP Investigation

### Show ICMP traffic

```text
icmp
```

**SOC use:** Investigate ping and other ICMP traffic.

### ICMP echo requests

```text
icmp.type == 8
```

**SOC use:** Identify ICMP echo requests in IPv4.

### ICMP echo replies

```text
icmp.type == 0
```

**SOC use:** Identify ICMP echo replies in IPv4.

---

## 10. Finding Large or Unusual Packets

### Large packets

```text
frame.len > 1000
```

**SOC use:** Focus on packets larger than a chosen size.

### Very large packets

```text
frame.len > 1400
```

**SOC use:** Investigate unusually large frames in the context of the traffic being analyzed.

> Packet size alone does not mean malicious activity. Always investigate the surrounding traffic and protocol.

---

## 11. TCP Streams

Right-click a TCP packet and select:

```text
Follow → TCP Stream
```

This can reconstruct the conversation associated with the TCP stream.

**SOC use:** Useful for understanding an individual TCP conversation, especially when analyzing unencrypted protocols.

> Do not assume that every visible stream is malicious. Analyze the content and context.

---

## 12. Conversations and Endpoints

Wireshark provides statistics that can help identify communicating systems.

Useful menus include:

```text
Statistics → Endpoints
Statistics → Conversations
```

**SOC use:**

- Identify hosts communicating with each other
- Find frequently communicating IP addresses
- Identify unusual connections
- Understand traffic relationships

---

## 13. Protocol Hierarchy

Use:

```text
Statistics → Protocol Hierarchy
```

This shows the protocols present in the capture.

**SOC use:** Quickly understand what types of traffic exist in a PCAP.

Example protocols may include:

```text
Ethernet
IPv4
TCP
UDP
DNS
HTTP
TLS
ICMP
```

---

## 14. Packet Details

Click a packet and inspect the packet details pane.

Look for:

```text
Source
Destination
Protocol
Source port
Destination port
Packet length
Flags
DNS information
HTTP information
TLS information
```

**SOC use:** Understand exactly what a packet contains and how the communication is structured.

---

## 15. Useful SOC Filters

### Traffic from one host

```text
ip.src == 10.2.8.194
```

### Traffic to one host

```text
ip.dst == 10.2.8.194
```

### TCP traffic

```text
tcp
```

### UDP traffic

```text
udp
```

### DNS

```text
dns
```

### HTTP

```text
http
```

### TLS

```text
tls
```

### ICMP

```text
icmp
```

### TCP port 22

```text
tcp.port == 22
```

### TCP port 80

```text
tcp.port == 80
```

### TCP port 443

```text
tcp.port == 443
```

### DNS + specific host

```text
dns && ip.addr == 10.2.8.194
```

### HTTP + specific host

```text
http && ip.addr == 10.2.8.194
```

### Traffic excluding one host

```text
ip.addr != 10.2.8.194
```

> Be careful with exclusion filters because they can hide traffic that may be relevant to an investigation.

---

# Quick SOC Analyst Reference

| Investigation question | Wireshark filter / feature |
|---|---|
| Show all IP traffic involving a host | `ip.addr == <IP>` |
| Show traffic from an IP | `ip.src == <IP>` |
| Show traffic to an IP | `ip.dst == <IP>` |
| Show TCP | `tcp` |
| Show UDP | `udp` |
| Show a TCP port | `tcp.port == <PORT>` |
| Show a UDP port | `udp.port == <PORT>` |
| Show DNS | `dns` |
| Show DNS queries | `dns.flags.response == 0` |
| Search for a domain | `dns.qry.name == "<domain>"` |
| Show HTTP | `http` |
| Show HTTP requests | `http.request` |
| Show TLS | `tls` |
| Show ICMP | `icmp` |
| Show TCP SYN packets | `tcp.flags.syn == 1` |
| Show large packets | `frame.len > 1000` |
| Inspect a TCP conversation | `Follow → TCP Stream` |
| Identify communicating hosts | `Statistics → Conversations` |
| Identify protocols | `Statistics → Protocol Hierarchy` |
| Identify network endpoints | `Statistics → Endpoints` |

---

# Basic PCAP Investigation Flow

```text
Open PCAP
    ↓
Statistics → Protocol Hierarchy
    ↓
What protocols are present?
    ↓
Statistics → Endpoints
    ↓
Which hosts are communicating?
    ↓
Statistics → Conversations
    ↓
Which connections stand out?
    ↓
Filter by IP
    ↓
Investigate the suspicious host
    ↓
Filter DNS / HTTP / TLS
    ↓
What domains or services are involved?
    ↓
Inspect TCP/UDP conversations
    ↓
Follow TCP Stream when appropriate
    ↓
Build a timeline
    ↓
Document findings
```

---

# Important SOC Mindset

A Wireshark alert or unusual packet is not automatically evidence of an attack.

Always ask:

1. **Who** is communicating?
2. **Who** are they communicating with?
3. **What protocol** is being used?
4. **Which port** is involved?
5. **When** did it happen?
6. **How often** did it happen?
7. **What data or metadata** is visible?
8. **Is the behavior expected?**
9. **What other evidence supports the finding?**

Wireshark is most useful when packet evidence is combined with other evidence such as endpoint logs, DNS logs, authentication logs, SIEM alerts, and threat intelligence.

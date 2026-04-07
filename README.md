# 🧑‍💻 Wireshark Network Traffic Analysis Project

This project demonstrates real network traffic analysis using Wireshark in a virtual lab environment.

Traffic was generated from an attacker machine (Kali Linux) and captured on a victim machine (Windows) using VMware Host-Only network.

The main objective is to understand normal vs suspicious traffic patterns and how a security analyst detects activities like port scanning, DNS queries, and ICMP behavior.


## 🛠 Tools Used
- Wireshark
- Nmap
- Kali Linux
- Windows
- VMware Workstation (Host-Only Network)
# 📁 PCAP Files & Analysis
   ##  1️⃣ ICMP Traffic (Ping Test)

File: 'icmp_traffic.pcapng'

From your screenshot:

- Multiple ICMP Echo Requests observed
- Message: “no response found”
- Continuous sequence numbers

## Filter used:

icmp

## 👉 Analysis:

- ICMP used for host discovery
- No replies indicate:
- Firewall blocking OR
- Target not responding
## 2️⃣ SYN Scan Detection (Port Scanning)

File: port_scan.pcapng

From your SYN scan screenshot:

- Multiple TCP packets with [SYN] flag
- Ports scanned:21, 25, 80, 135, 8080, etc.

## Filter used:

tcp.flags.syn == 1 && tcp.flags.ack == 0

## 👉 Analysis:

- Clear Nmap SYN scan behavior
- Attacker checking open ports
- This is reconnaissance activity
## 3️⃣ DNS Query / DNS Behavior

File: dns_anomaly.pcapng

From your DNS screenshots:

- Queries for:
     - debian.pool.ntp.org
     - .localdomain
- Protocol: UDP (Port 53)

## Filter used:

dns

## 👉 Analysis:

- Continuous DNS queries observed
- No response due to Host-Only network
- Demonstrates DNS anomaly / no resolution
## 🟢 4️⃣ ICMP + DNS Combined Analysis

File: icmp_dns.pcapng

From your combined filter screenshot:

- ICMP requests + DNS queries together

## Filter used:

icmp || dns

## 👉 What Observed:

- ICMP → Host discovery
- DNS → Name resolution attempts

## 👉 Analysis:
 Shows how attacker:
- 1.Checks host availability (ICMP)
- 2.Tries resolving domains (DNS)
## 🔵 5️⃣ TCP Handshake + HTTP + Keep-Alive

File: tcp_handshake_http_keepalive.pcapng

From your last screenshot:

## Filter used:

tcp.port == 9000

## 👉 Observed:

✔ TCP 3-Way Handshake
- SYN
- SYN-ACK
- ACK
✔ HTTP Communication
- GET / HTTP/1.1 request
✔ TCP Keep-Alive
- Keep-Alive packets
- ACK responses

## 👉 Analysis:

- Connection successfully established
- HTTP communication working
- Session maintained using Keep-Alive
## ⚖️ Protocol Understanding
- ICMP → Host discovery (Ping)
- DNS (UDP) → Fast name resolution
- TCP → Reliable communication
- SYN Scan → Port scanning technique
## 🚨 Security Findings
- Multiple SYN packets → Port Scanning Detected
- ICMP no response → Firewall / Filtering
- DNS without response → Network limitation / anomaly
## 🎯 Learning Outcome
- Packet-level traffic analysis
- Identifying SYN scan patterns
- Understanding DNS behavior
- Using Wireshark filters
- SOC-level investigation basics
# 📌 Conclusion

## This project simulates real-world attacker and victim communication and demonstrates how a security analyst can detect suspicious activities using Wireshark packet analysis.

# 👤 Author

## Umang Patidar

# Network Traffic Analysis — Zeek + tcpdump

## Project Overview
Captured and analyzed live network traffic on a macOS device using 
tcpdump and Zeek. Identified connection patterns, DNS behavior, 
TLS usage, and network anomalies.

## Tools Used
- tcpdump — packet capture
- Zeek — network traffic analyzer
- macOS en0 (Wi-Fi interface)

## Capture Details
| Field | Value |
|---|---|
| Date | 22 April 2025 |
| Interface | en0 (Wi-Fi) |
| Local IP | 192.168.0.33 |
| Duration | 60 seconds |
| Packets captured | 8,072 |
| Packets dropped | 0 |
| Connections analyzed | 182 |

## Key Findings

### 1. All traffic encrypted with TLS 1.3
106 out of 106 HTTPS connections used TLS 1.3 — 
the latest and most secure protocol version. 
No deprecated TLS 1.0 or 1.1 detected.

### 2. No suspicious external IPs
All external connections resolved to Apple Inc 
and Fastly CDN infrastructure. No unknown or 
blacklisted IPs contacted.

### 3. No DNS tunneling detected
DNS queries were limited to Apple service discovery 
and iCloud endpoints. No long randomized domain 
names associated with DNS tunneling.

### 4. QUIC protocol detected
Zeek flagged 7 QUIC anomalies — consistent with 
background browser activity using Google's QUIC 
protocol. Low severity, expected behavior.

### 5. Minor TCP anomalies
Two low-severity TCP anomalies detected 
(sequence underflow, window recision) — 
common on Wi-Fi networks, not indicative of attack.

## Log Files Analyzed
| Log | Description |
|---|---|
| conn.log | All TCP/UDP connections |
| dns.log | DNS queries and responses |
| ssl.log | TLS/HTTPS connection details |
| quic.log | QUIC protocol traffic |
| weird.log | Anomalies flagged by Zeek |

## Methodology
1. Captured 60 seconds of live traffic using tcpdump on en0
2. Analyzed pcap with Zeek to generate structured logs
3. Queried logs using zeek-cut for DNS, TLS, IP analysis
4. Documented findings and anomalies

## Conclusion
No malicious activity detected. Network traffic consistent 
with normal macOS background activity — primarily iCloud 
sync, Apple metrics, and software update checks.

# Wireshark Network Traffic Analysis Lab

## Overview

This lab demonstrates how to capture and analyze baseline network traffic using **Wireshark**. The goal was to observe normal network behavior from my system, identify common protocols, and understand how encrypted web traffic appears during normal browsing activity.

Establishing a **baseline of normal network traffic** is an important skill for SOC analysts because it helps identify abnormal or malicious activity during investigations.

---

## Lab Environment

**Host System:** macOS  
**Capture Interface:** Wi-Fi (en0)  
**Tool Used:** Wireshark  
**Capture Duration:** ~3–5 minutes  

Traffic was generated through normal browsing activity to simulate everyday network behavior.

---

## Objectives

- Capture live network traffic using Wireshark  
- Identify common protocols in baseline traffic  
- Analyze DNS queries and responses  
- Observe TLS handshake behavior for encrypted connections  
- Reconstruct client-server conversations using TCP Stream  
- Investigate captured traffic for potential suspicious activity  

---

## Protocols Observed

| Protocol | Purpose |
|--------|--------|
| DNS | Resolves domain names to IP addresses |
| TCP | Reliable transport protocol used by many applications |
| TLS | Encryption used for secure HTTPS connections |
| QUIC | Transport protocol used for HTTP/3 connections |

---

## DNS Analysis

Using the Wireshark display filter:


dns


I observed multiple DNS queries resolving domains used by common cloud services.

Examples included:

- `googleapis.com`
- `ssl.gstatic.com`
- `icloud.com`

This demonstrates how systems resolve domain names before establishing connections to remote servers.

**Evidence screenshot:**  
`dns-filter.png`

---

## TLS Handshake Analysis

Using the filter:


tls


I observed encrypted HTTPS sessions including:

- **Client Hello**
- **Server Hello**
- **Encrypted Application Data**

These exchanges confirm secure HTTPS communication between the client and external services.

Because the traffic is encrypted, payload contents are not visible, which is expected behavior for TLS-secured communication.

**Evidence screenshot:**  
`tls-handshake.png`

---

## Host Traffic Isolation

To analyze traffic generated specifically by my machine, I used the following filter:


ip.addr == 10.0.0.13


This allowed me to isolate client traffic and observe communication between my system and external servers.

**Evidence screenshot:**  
`ip-filter.png`

---

## TCP Stream Analysis

Using the **Follow TCP Stream** feature in Wireshark, I reconstructed the full client-server conversation.

This confirmed that the connection contained encrypted TLS data, indicating secure HTTPS traffic between the client and remote services.

**Evidence screenshot:**  
`tcp-stream.png`

---

## Threat Detection Investigation

Captured traffic was also reviewed for potential suspicious activity.

Checks performed included:

- Identifying unusual DNS queries
- Reviewing external IP connections
- Checking for abnormal port usage
- Observing repeated connection patterns

Filters used during this process included:


dns
tcp.port != 443
tcp.port != 80


### Result

No malicious or suspicious activity was detected during this capture.

All observed traffic resolved to legitimate services including:

- Google APIs
- Apple iCloud services
- Other standard web services

This confirms that the traffic captured represents **normal baseline network behavior**.

---

## Key Takeaways

- DNS traffic reveals which domains systems communicate with.
- TLS encryption protects the contents of network communication.
- Baseline traffic analysis helps security teams recognize abnormal activity.
- Wireshark is a powerful tool for investigating network communication and security incidents.

---

## Skills Demonstrated

- Network traffic capture
- Protocol analysis
- DNS investigation
- TLS handshake analysis
- TCP stream reconstruction
- Baseline network behavior analysis
- Wireshark filtering techniques

---

## Evidence

Screenshots and capture files are included in the repository.


evidence/
├── dns-filter.png
├── tls-handshake.png
├── ip-filter.png
├── tcp-stream.png

pcaps/
└── baseline-browsing.pcapng

---
# Author

Femi Ijatoye  
Security+ Certified  
Cybersecurity / SOC Analyst Portfolio Project

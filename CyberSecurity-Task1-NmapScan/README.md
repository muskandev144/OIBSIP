# Task 1 · Basic Network Scanning with Nmap

## What is Nmap?
Nmap (Network Mapper) is a free, open-source tool used to discover devices on a network, identify open ports, and detect which services and operating systems are running on those devices. It is widely used by security professionals, system administrators, and ethical hackers for network security assessments.

## Why Network Scanning Matters
Network scanning helps identify:
- Which ports are open and potentially exposed to attackers
- What services are running and whether they are outdated or vulnerable
- The operating system in use, which helps assess known vulnerabilities
- Unauthorized devices or services on a network

Regular scanning allows administrators to close unnecessary ports, patch vulnerable services, and reduce the overall attack surface of a system.

## Ethical Use Guidelines
⚠️ Network scanning should only be performed on:
- Systems you personally own
- Systems you have explicit written permission to test

Scanning external, third-party, or production systems without authorization is illegal and unethical. This task was performed entirely on `127.0.0.1` (localhost), which is the user's own machine.

## Scans Performed

### 1. Service Version Scan
Command: `nmap -sV 127.0.0.1`

| Port | State | Service | Version |
|------|-------|---------|---------|
| 135/tcp | open | msrpc | Microsoft Windows RPC |
| 445/tcp | open | microsoft-ds | — |
| 3306/tcp | open | mysql | MySQL 8.0.45 |
| 5432/tcp | open | postgresql | PostgreSQL DB |

**Security Analysis:**
- **Port 135 (RPC):** Used for internal Windows communication. If exposed externally, it can be exploited for remote code execution attacks.
- **Port 445 (SMB):** One of the most commonly attacked ports (e.g., WannaCry ransomware used this port). Should never be exposed to the internet.
- **Port 3306 (MySQL):** Database port. Risk of unauthorized access if weak credentials are used.
- **Port 5432 (PostgreSQL):** Database port. Same risk as above — should be firewalled from public access.

### 2. OS Detection Scan
Command: `nmap -O 127.0.0.1`

**Result:**
- Device type: General purpose
- Running: Microsoft Windows 11
- OS details: Microsoft Windows 11 24H2 – 25H2

## Conclusion
This scan confirmed that several services are running on the local machine, including two database servers (MySQL, PostgreSQL) and Windows networking services (RPC, SMB). In a production environment, these ports should be restricted using a firewall and only exposed to trusted internal networks.

## Tools Used
- Nmap 7.991
- Windows 11, Command Prompt

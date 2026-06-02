# Unit 3: Vulnerability Scanning

---

## 3.1 Planning the Vulnerability Scan

### What is Vulnerability Scanning?
Vulnerability scanning is the process of **identifying, quantifying, and prioritizing** security vulnerabilities in systems, networks, and applications. Unlike penetration testing, vulnerability scanning is mostly **automated** and does not involve active exploitation.

### Pre-Scan Planning:
- **Define scope** – Which systems, networks, and applications to scan
- **Identify scan targets** – IP ranges, domains, specific hosts
- **Schedule scans** – Avoid disrupting business operations
- **Obtain authorization** – Written permission required
- **Select appropriate tools** – Based on target type
- **Configure scan parameters** – Intensity, timing, credentials

### Scan Considerations:
- **Credentialed vs. Non-Credentialed Scans**

| Type | Description | Depth | Accuracy |
|---|---|---|---|
| **Credentialed (Authenticated)** | Uses valid credentials to log into the target | Deep | High – finds more vulnerabilities |
| **Non-Credentialed (Unauthenticated)** | Scans from outside without credentials | Surface | Lower – may miss internal issues |

---

## 3.2 Types of Scans

| Scan Type | Description |
|---|---|
| **Network Scan** | Identifies live hosts, open ports, and running services on a network |
| **Port Scan** | Identifies open/closed/filtered ports on a target |
| **Vulnerability Scan** | Identifies known vulnerabilities in systems and software |
| **Web Application Scan** | Scans web apps for vulnerabilities (SQLi, XSS, etc.) |
| **Wireless Scan** | Identifies wireless access points, encryption types, rogue APs |
| **Compliance Scan** | Checks systems against regulatory standards (PCI-DSS, HIPAA) |
| **Discovery Scan** | Maps the network to find all connected devices |

### Port Scan Types (Nmap):

| Scan Type | Flag | Description |
|---|---|---|
| **TCP Connect Scan** | `-sT` | Full TCP handshake (SYN → SYN-ACK → ACK) |
| **SYN Scan (Stealth)** | `-sS` | Half-open scan; sends SYN, receives SYN-ACK, sends RST (default for root) |
| **UDP Scan** | `-sU` | Scans UDP ports (slower than TCP) |
| **FIN Scan** | `-sF` | Sends FIN flag; stealthy, used to bypass firewalls |
| **XMAS Scan** | `-sX` | Sends FIN, PSH, URG flags; used to bypass firewalls |
| **NULL Scan** | `-sN` | Sends no flags; used to bypass firewalls |
| **ACK Scan** | `-sA` | Used to determine firewall rules (filtered vs unfiltered) |
| **Ping Scan** | `-sn` | Host discovery only, no port scan |
| **Version Detection** | `-sV` | Determines service version running on open ports |
| **OS Detection** | `-O` | Attempts to identify the target's operating system |

---

## 3.3 Detecting Defenses

### Common Defenses to Detect:
- **Firewalls** – Filter traffic based on rules; detected via ACK scans
- **Intrusion Detection Systems (IDS)** – Monitors network for suspicious activity (passive)
- **Intrusion Prevention Systems (IPS)** – Monitors AND blocks suspicious activity (active)
- **Web Application Firewalls (WAF)** – Protects web applications
- **Antivirus / Endpoint Protection** – Detects malware on endpoints
- **Honeypots / Honeynets** – Decoy systems to detect attackers

### How to Detect Firewalls:
- **ACK Scan (`-sA`)** – Determines if ports are filtered or unfiltered
- **Traceroute** – Shows network path and potential filtering devices
- **TTL analysis** – Differences in TTL values can reveal firewall presence

---

## 3.4 Analyzing the Attack Surface

The **attack surface** is the sum of all possible entry points where an unauthorized user can try to enter or extract data.

### Components:
- **Network attack surface** – Open ports, services, protocols
- **Software attack surface** – Applications, APIs, web services
- **Human attack surface** – Employees susceptible to social engineering
- **Physical attack surface** – Physical access points

---

## 3.5 Crafting Packets

**Packet crafting** involves creating custom network packets to test security controls and bypass defenses.

### Tools for Packet Crafting:

| Tool | Description |
|---|---|
| **Scapy** | Python-based packet crafting and manipulation tool |
| **hping3** | Command-line packet crafting tool |
| **Nping** | Part of Nmap suite; packet generation and response analysis |
| **PackETH** | GUI-based Ethernet packet generator |
| **Colasoft Packet Builder** | GUI packet builder for Windows |

---

## 3.6 Network Traffic Analysis

### What is Network Traffic Analysis?
Analyzing captured network traffic to identify vulnerabilities, suspicious activity, and security issues.

### Key Protocols and Ports:

| Port | Protocol/Service | Description |
|---|---|---|
| 20/21 | FTP | File Transfer Protocol |
| 22 | SSH | Secure Shell |
| 23 | Telnet | Unencrypted remote access |
| 25 | SMTP | Email sending |
| 53 | DNS | Domain Name System |
| 67/68 | DHCP | Dynamic Host Configuration |
| 80 | HTTP | Web traffic (unencrypted) |
| 88 | Kerberos | Authentication protocol |
| 110 | POP3 | Email retrieval |
| 135 | RPC | Remote Procedure Call |
| 139 | NetBIOS | Network Basic I/O System |
| 143 | IMAP | Email retrieval |
| 389 | LDAP | Directory services |
| 443 | HTTPS | Secure web traffic |
| 445 | SMB | Server Message Block (file sharing) |
| 464 | Kerberos | Password change |
| 993 | IMAPS | Secure IMAP |
| 995 | POP3S | Secure POP3 |
| 1433 | MSSQL | Microsoft SQL Server |
| 3306 | MySQL | MySQL Database |
| 3389 | RDP | Remote Desktop Protocol |
| 5432 | PostgreSQL | PostgreSQL Database |
| 8080 | HTTP Proxy | Alternative HTTP port |

### Identifying Servers by Open Ports:

| Ports Open | Likely Server Type |
|---|---|
| 88, 135, 139, 389, 464 | **Domain Controller** (Active Directory) |
| 25, 110, 143 | **Email Server** |
| 80, 443 | **Web Server** |
| 21 | **FTP Server** |
| 22 | **SSH Server** |
| 445 | **SMB/File Server** |
| 3389 | **Windows with RDP** |

### ARP Analysis:

**ARP (Address Resolution Protocol)** maps IP addresses to MAC addresses.

- **ARP Spoofing/Poisoning** – Attacker sends fake ARP messages to link their MAC with a legitimate IP
- **Indicator of ARP Spoofing:** **Multiple MAC addresses for a single IP** or **duplicate IP addresses in ARP table**

---

## 3.7 Evaluating Wireless Network Traffic

### Wireless Security Protocols:

| Protocol | Security Level | Description |
|---|---|---|
| **WEP** | Very Weak | Easily crackable; uses RC4 encryption |
| **WPA** | Moderate | Uses TKIP; improvement over WEP |
| **WPA2** | Strong | Uses AES-CCMP encryption |
| **WPA3** | Strongest | Uses SAE (Simultaneous Authentication of Equals) |

### Wireless Attacks:
- **Evil Twin** – Setting up a rogue access point mimicking a legitimate one
- **Deauthentication Attack** – Forcing clients to disconnect from a network
- **WPS Pin Attack** – Exploiting Wi-Fi Protected Setup
- **KARMA Attack** – Responding to probe requests from devices
- **Wardriving** – Driving around to discover wireless networks

### Wireless Scanning Tools:
- **Aircrack-ng** – Wireless network cracking suite
- **Kismet** – Wireless network detector and sniffer
- **WiFite** – Automated wireless auditing tool
- **inSSIDer** – Wi-Fi network scanner

---

## 3.8 Scanning Tools

### Nmap (Network Mapper)
- **Purpose:** Network discovery and security auditing
- **Features:** Port scanning, OS detection, version detection, scripting engine (NSE)
- **Usage:**
  ```
  nmap -sS -sV -O 192.168.1.0/24    # SYN scan with version and OS detection
  nmap -sn 192.168.1.0/24            # Ping sweep (host discovery)
  nmap -p 1-65535 192.168.1.1        # Full port scan
  nmap -A 192.168.1.1                # Aggressive scan (OS, version, scripts, traceroute)
  nmap --script vuln 192.168.1.1     # Run vulnerability scripts
  ```

### Nmap Scripting Engine (NSE)
- **Purpose:** Extends Nmap's capabilities with scripts
- **Categories:** auth, broadcast, discovery, exploit, vuln, safe, intrusive
- **Usage:**
  ```
  nmap --script=http-title 192.168.1.1        # Get HTTP page titles
  nmap --script=smb-vuln-ms17-010 192.168.1.1 # Check for EternalBlue
  ```

### Nikto
- **Purpose:** Web server vulnerability scanner
- **Features:** Checks for dangerous files, outdated software, server misconfigurations
- **Usage:** `nikto -h http://target.com`

### Nessus
- **Purpose:** Comprehensive vulnerability scanner
- **Features:** Network, web app, and compliance scanning
- **Key Feature:** Provides CVSS scores and remediation advice
- **Usage:** Web-based GUI interface

### Other Scanning Tools:

| Tool | Purpose |
|---|---|
| **OpenVAS** | Open-source vulnerability scanner |
| **Qualys** | Cloud-based vulnerability management |
| **Nexpose (Rapid7)** | Vulnerability management platform |
| **Wireshark** | Network protocol analyzer (packet capture) |
| **tcpdump** | Command-line packet capture |
| **Masscan** | Ultra-fast port scanner |
| **Enum4linux** | SMB/Samba enumeration |

---

## 3.9 Evading Detection and Covering Tracks

### Evasion Techniques:
- **Fragmentation** – Splitting packets into smaller fragments to bypass IDS
- **Decoy scanning** – Using fake source IPs (`nmap -D RND:10`)
- **Timing attacks** – Slowing down scans to avoid detection (`nmap -T0`)
- **Proxy chains** – Routing traffic through multiple proxies
- **Encryption** – Using encrypted channels (SSH tunnels, VPN)
- **Encoding payloads** – Obfuscating malicious payloads

### Covering Tracks:
- **Clearing logs** – Removing entries from system logs
- **Modifying timestamps** – Changing file modification times
- **Using rootkits** – Hiding malicious activity from the OS
- **Disabling auditing** – Turning off logging mechanisms

### Nmap Timing Options:

| Flag | Name | Speed | Stealth |
|---|---|---|---|
| `-T0` | Paranoid | Very slow | Most stealthy |
| `-T1` | Sneaky | Slow | Very stealthy |
| `-T2` | Polite | Below normal | Stealthy |
| `-T3` | Normal | Default | Normal |
| `-T4` | Aggressive | Fast | Less stealthy |
| `-T5` | Insane | Very fast | Least stealthy |

---

## MCQ Practice Questions

---

**Q1.** In ARP analysis, what could indicate a possible ARP spoofing attack?

A. Duplicate IP addresses in the ARP table  
B. Missing MAC addresses in the ARP table  
**C. Multiple MAC addresses for a single IP** ✅  
D. Unusual DNS queries

> **Explanation:** ARP spoofing causes multiple MAC addresses to be associated with a single IP address in the ARP table.

---

**Q2.** As part of a gray box penetration test, you need to capture packets on a wired network. You've configured the network interface in your laptop to accept all frames transmitted on the network medium, and you have installed Wireshark. However, when you run Wireshark, you only see frames that are addressed specifically to your laptop. Why did this happen?

A. A host-based firewall on your laptop is blocking all other frames  
B. MAC address filtering has been enabled on the switch  
C. The network uses a hub  
**D. The network uses a switch** ✅

> **Explanation:** A switch sends frames only to the intended recipient's port (unlike a hub which broadcasts to all ports). Even in promiscuous mode, a switch limits what you can see.

---

**Q3.** You are performing reconnaissance as part of a gray box penetration test. You run a vulnerability scan on one of the target organization's servers and discover that several ports are open, including 88, 135, 139, 389, and 464. What does this indicate?

**A. It is a domain controller** ✅  
B. It is a POP3 email server  
C. It is an SSH server  
D. It is an IMAP email server

> **Explanation:** Ports 88 (Kerberos), 135 (RPC), 139 (NetBIOS), 389 (LDAP), and 464 (Kerberos password change) are characteristic of an Active Directory Domain Controller.

---

**Q4.** You run a vulnerability scan on one of the target organization's internal servers and discover that port 445 is open. What service is likely running?

A. FTP  
B. SSH  
**C. SMB (Server Message Block)** ✅  
D. HTTP

> **Explanation:** Port 445 is used for SMB (Server Message Block), which provides file sharing and network communication on Windows systems.

---

**Q5.** Which Nmap scan type performs a half-open (stealth) scan?

A. `-sT` (TCP Connect)  
**B. `-sS` (SYN Scan)** ✅  
C. `-sU` (UDP Scan)  
D. `-sA` (ACK Scan)

> **Explanation:** The SYN scan (`-sS`) is called a "stealth" or "half-open" scan because it doesn't complete the full TCP handshake – it sends RST after receiving SYN-ACK.

---

**Q6.** Which tool is specifically designed for web server vulnerability scanning?

A. Nmap  
**B. Nikto** ✅  
C. Wireshark  
D. Aircrack-ng

> **Explanation:** Nikto is specifically designed to scan web servers for vulnerabilities, misconfigurations, and outdated software.

---

**Q7.** What is the purpose of a credentialed vulnerability scan?

A. To scan without any authentication  
**B. To scan with valid credentials for deeper vulnerability assessment** ✅  
C. To test password strength  
D. To perform social engineering

> **Explanation:** Credentialed scans use valid login credentials to access the system from inside, allowing for deeper and more accurate vulnerability detection.

---

**Q8.** Which wireless security protocol uses AES-CCMP encryption?

A. WEP  
B. WPA  
**C. WPA2** ✅  
D. None of the above

> **Explanation:** WPA2 uses AES-CCMP (Counter Mode with CBC-MAC Protocol) for encryption, providing strong security.

---

**Q9.** You want to scan all 65535 ports on a target. Which Nmap command would you use?

A. `nmap -sS target`  
**B. `nmap -p 1-65535 target`** ✅  
C. `nmap -sn target`  
D. `nmap -O target`

> **Explanation:** The `-p 1-65535` flag tells Nmap to scan all TCP ports from 1 to 65535.

---

**Q10.** What does the Nmap `-sn` flag do?

A. Performs a SYN scan  
B. Performs a NULL scan  
**C. Performs host discovery only (ping scan, no port scan)** ✅  
D. Performs a stealth scan

> **Explanation:** The `-sn` flag tells Nmap to perform host discovery (ping sweep) without scanning ports.

---

**Q11.** Which Nmap timing option provides the most stealthy scan?

**A. `-T0` (Paranoid)** ✅  
B. `-T3` (Normal)  
C. `-T4` (Aggressive)  
D. `-T5` (Insane)

> **Explanation:** `-T0` (Paranoid) is the slowest and most stealthy timing option, designed to evade IDS detection.

---

**Q12.** Which technique can be used to evade intrusion detection systems during scanning?

A. Using default scan settings  
B. Scanning from a single IP  
**C. Packet fragmentation** ✅  
D. Using TCP connect scans

> **Explanation:** Packet fragmentation splits packets into smaller pieces, making it harder for IDS to reassemble and analyze them.

---

**Q13.** What is the purpose of Nmap Scripting Engine (NSE)?

A. To encrypt scan results  
B. To speed up scans  
**C. To extend Nmap's capabilities with automated scripts** ✅  
D. To create custom ports

> **Explanation:** NSE allows users to run scripts for vulnerability detection, enumeration, and various other tasks.

---

**Q14.** Which tool is used for network protocol analysis and packet capture?

A. Nmap  
B. Nikto  
**C. Wireshark** ✅  
D. Nessus

> **Explanation:** Wireshark is the most popular network protocol analyzer, used for capturing and analyzing network traffic.

---

**Q15.** An Nmap ACK scan (`-sA`) is primarily used for:

A. Finding open ports  
B. Detecting OS versions  
**C. Determining firewall rules (filtered vs. unfiltered)** ✅  
D. Performing DNS lookups

> **Explanation:** ACK scans are used to map firewall rules and determine which ports are filtered or unfiltered.

---

**Q16.** Which of the following is NOT a valid evasion technique?

A. Fragmentation  
B. Decoy scanning  
C. Using proxy chains  
**D. Increasing scan speed** ✅

> **Explanation:** Increasing scan speed actually makes it easier to detect. Slowing scans down (`-T0`, `-T1`) is an evasion technique.

---

**Q17.** What type of attack involves setting up a rogue access point that mimics a legitimate Wi-Fi network?

A. Deauthentication attack  
B. WPS attack  
**C. Evil Twin attack** ✅  
D. Wardriving

> **Explanation:** An Evil Twin attack creates a fake access point with the same SSID as a legitimate network to trick users into connecting.

---

**Q18.** Which Nmap scan sends packets with FIN, PSH, and URG flags set?

A. NULL Scan  
B. FIN Scan  
**C. XMAS Scan** ✅  
D. ACK Scan

> **Explanation:** The XMAS scan (`-sX`) sends packets with FIN, PSH, and URG flags set (like a lit-up Christmas tree).

---

**Q19.** Nessus provides vulnerability scores using which scoring system?

A. CVE  
B. CWE  
**C. CVSS (Common Vulnerability Scoring System)** ✅  
D. NVD

> **Explanation:** Nessus uses CVSS scores to rate the severity of discovered vulnerabilities.

---

**Q20.** Which scan type would give the MOST information about a target including OS, services, scripts, and traceroute?

A. `-sS`  
B. `-sV`  
**C. `-A` (Aggressive scan)** ✅  
D. `-sn`

> **Explanation:** The `-A` flag enables OS detection, version detection, script scanning, and traceroute all in one aggressive scan.

---

# Unit 6: Communication & Reporting, Active Directory Attacks, IoT Attacks

---

## Part A: Communication and Reporting

---

## 6.1 Communication Path

### During a Penetration Test:
Communication must be structured and follow predefined channels:

- **Primary Contact** – Main point of contact at the client organization
- **Technical Contact** – IT/Security team member for technical issues
- **Emergency Contact** – For critical situations (system down, data breach)
- **Management Contact** – Executive sponsor of the engagement

### Communication Guidelines:
- Use **encrypted communication** channels (encrypted email, secure messaging)
- Follow the **communication plan** defined in the ROE
- Document all communications
- Never share findings over insecure channels
- Maintain confidentiality at all times

---

## 6.2 Communication Triggers

### When to Communicate Immediately:
| Trigger | Action |
|---|---|
| **Critical vulnerability found** | Notify client immediately – do not wait for the report |
| **System crash or outage** | Stop testing and notify emergency contact |
| **Data breach discovered** | Immediate escalation to management |
| **Evidence of active compromise** | Alert client – another attacker may already be in the system |
| **Scope creep** | Discuss with client before proceeding |
| **Out-of-scope system accidentally accessed** | Notify immediately and document |
| **Indicators of prior compromise** | Report signs of existing breach (unknown accounts, backdoors) |

> **Key Point:** If you find an **existing, active breach** during a pentest, you must report it immediately. This is a critical communication trigger.

---

## 6.3 Reporting Tools

| Tool | Purpose |
|---|---|
| **Dradis** | Collaborative reporting platform for security assessments |
| **Faraday** | Vulnerability management and collaboration platform |
| **Serpico** | Report generation tool for pentest findings |
| **PlexTrac** | Security reporting and analytics platform |
| **Pwndoc** | Pentest report generator |
| **Ghostwriter** | Reporting and tracking for red team operations |
| **Microsoft Word/Excel** | Traditional reporting format |
| **CherryTree** | Hierarchical note-taking for pentest documentation |

---

## 6.4 Identifying Report Audience

### Audience Types:

| Audience | What They Need | Level of Detail |
|---|---|---|
| **C-Suite / Executives** | Business impact, risk overview, high-level recommendations | High-level summary |
| **Management** | Risk prioritization, remediation costs, timeline | Moderate detail |
| **Technical Team (IT/DevOps)** | Detailed findings, steps to reproduce, technical remediation | Full technical detail |
| **Compliance / Legal** | Compliance status, regulatory gaps, legal implications | Compliance-focused |
| **Third-party Stakeholders** | Certification, assurance of security posture | Summary with certification |

> **Key Point:** Always tailor the report to the audience. An executive summary differs vastly from a technical appendix.

---

## 6.5 Report Content

### Standard Pentest Report Structure:

#### 1. Executive Summary
- High-level overview of findings
- Business impact assessment
- Overall risk rating
- Key recommendations
- Written for non-technical stakeholders

#### 2. Scope and Methodology
- Systems tested (in-scope)
- Systems excluded (out-of-scope)
- Testing methodology used (PTES, OWASP, etc.)
- Tools used
- Testing timeline

#### 3. Findings Summary
- Total vulnerabilities by severity (Critical, High, Medium, Low, Informational)
- Risk ratings (CVSS scores)
- Categorization of vulnerabilities

#### 4. Detailed Findings
For each vulnerability:
- **Title** – Clear, descriptive name
- **Severity/Risk Rating** – Critical, High, Medium, Low
- **CVSS Score** – Numerical risk score
- **Description** – What the vulnerability is
- **Impact** – What could happen if exploited
- **Proof of Concept (PoC)** – Evidence/screenshots showing exploitation
- **Affected Systems** – Which systems are vulnerable
- **Remediation** – How to fix the vulnerability
- **References** – CVE numbers, external resources

#### 5. Remediation Recommendations
- Prioritized list of fixes
- Short-term vs. long-term recommendations
- Estimated effort for each fix

#### 6. Appendices
- Raw tool output
- Screenshots
- Network diagrams
- Full scan results

### CVSS Severity Ratings:

| Score | Rating | Description |
|---|---|---|
| 0.0 | None | No impact |
| 0.1 – 3.9 | Low | Minor risk |
| 4.0 – 6.9 | Medium | Moderate risk |
| 7.0 – 8.9 | High | Significant risk |
| 9.0 – 10.0 | Critical | Severe, immediate risk |

---

## 6.6 Presentation of Findings

### Best Practices:
- **Prioritize findings** by risk level (Critical → High → Medium → Low)
- **Use visual aids** – Charts, graphs, risk matrices
- **Include screenshots** – Proof of exploitation
- **Demonstrate business impact** – Not just technical severity
- **Provide actionable remediation** – Specific steps, not generic advice
- **Use consistent formatting** – Professional, readable layout
- **Include a risk matrix** – Visual representation of likelihood vs. impact

---

## 6.7 Best Practices for Reports

- **Be objective** – Report facts, not opinions
- **Be accurate** – Verify all findings before reporting
- **Be clear** – Avoid unnecessary jargon for non-technical audiences
- **Be concise** – Include necessary detail without being verbose
- **Include evidence** – Screenshots, logs, packet captures
- **Normalize risk ratings** – Use consistent CVSS scoring
- **Review before delivery** – Proofread and validate all findings
- **Secure delivery** – Encrypt the report; use secure file transfer
- **Handle data carefully** – Delete test data and credentials after engagement

---

## 6.8 Recommending Remediation

### Remediation Priority Framework:

| Priority | Criteria | Timeline |
|---|---|---|
| **Immediate (P1)** | Critical vulnerabilities with active exploitation | 24-48 hours |
| **High (P2)** | High-risk vulnerabilities exploitable remotely | 1-2 weeks |
| **Medium (P3)** | Medium-risk requiring specific conditions | 1-3 months |
| **Low (P4)** | Low-risk, informational findings | Next scheduled update |

### Common Remediation Recommendations:
- **Patch management** – Apply security patches regularly
- **Input validation** – Sanitize all user inputs
- **Least privilege** – Minimize user and service permissions
- **Network segmentation** – Isolate critical systems
- **Multi-factor authentication (MFA)** – Enforce for all accounts
- **Encryption** – Encrypt data at rest and in transit
- **Security awareness training** – Educate employees on social engineering
- **Monitoring and logging** – Implement comprehensive logging

---

## 6.9 Post-Report Delivery Activities

- **Debrief meeting** – Walk through findings with stakeholders
- **Remediation verification** – Retest after fixes are applied
- **Cleanup** – Remove all tools, backdoors, test accounts, and test data
- **Data destruction** – Securely delete all captured sensitive data
- **Attestation letter** – Provide formal attestation if required
- **Lessons learned** – Document what went well and what to improve
- **Follow-up assessment** – Schedule retesting after remediation

---

## Part B: Attacks on IoT Devices

---

## 6.10 IoT (Internet of Things) Security

### What is IoT?
IoT refers to interconnected devices that communicate and exchange data over the internet (smart thermostats, cameras, medical devices, industrial sensors).

### IoT Attack Surfaces:

| Surface | Examples |
|---|---|
| **Device Hardware** | Debug ports (JTAG, UART), exposed memory chips |
| **Firmware** | Hardcoded credentials, unencrypted firmware updates |
| **Network** | Unencrypted protocols, weak Wi-Fi security |
| **Web Interface** | Default credentials, XSS, SQLi in management interface |
| **Mobile App** | Insecure API communication, local storage |
| **Cloud Backend** | Misconfigured APIs, weak authentication |
| **Communication Protocols** | MQTT, CoAP, Zigbee, Z-Wave vulnerabilities |

### Common IoT Vulnerabilities:
- **Default/weak credentials** – admin/admin, admin/password
- **Lack of encryption** – Data transmitted in plaintext
- **No firmware update mechanism** – Unable to patch vulnerabilities
- **Insecure network services** – Exposed Telnet, FTP, SSH
- **Lack of authentication** – No authentication for critical functions
- **Hardcoded credentials** – Cannot be changed by user
- **Physical security issues** – Physical access to debug ports

### IoT Attack Tools:

| Tool | Purpose |
|---|---|
| **Shodan** | Discover exposed IoT devices |
| **Firmware Analysis Toolkit (FAT)** | Analyze IoT firmware |
| **Binwalk** | Firmware analysis and extraction |
| **Attify** | IoT penetration testing framework |
| **MQTT Explorer** | Analyze MQTT protocol traffic |
| **HackRF** | Software-defined radio for wireless analysis |
| **Zigbee Sniffer** | Capture Zigbee protocol traffic |

---

## Part C: Active Directory Attacks

---

## 6.11 Kerberos Authentication

### How Kerberos Works:
Kerberos is the default authentication protocol in Active Directory.

#### Key Components:
- **KDC (Key Distribution Center)** – Authentication server (runs on Domain Controller)
- **AS (Authentication Service)** – Verifies user credentials
- **TGS (Ticket Granting Service)** – Issues service tickets
- **TGT (Ticket Granting Ticket)** – Initial ticket from AS
- **Service Ticket (ST)** – Ticket for accessing a specific service

#### Kerberos Authentication Flow:
1. **AS-REQ** → User sends authentication request to KDC
2. **AS-REP** → KDC sends TGT (encrypted with user's password hash)
3. **TGS-REQ** → User sends TGT to request a service ticket
4. **TGS-REP** → KDC sends service ticket
5. **AP-REQ** → User presents service ticket to the service
6. **AP-REP** → Service grants access

### Kerberos Authentication Flaws:
- TGT encrypted with **krbtgt** account hash – if compromised, all tickets can be forged
- Service tickets encrypted with **service account's** NTLM hash
- Pre-authentication can be disabled (enables AS-REP Roasting)
- Weak service account passwords enable Kerberoasting

---

## 6.12 Kerberoasting

### What is Kerberoasting?
Kerberoasting extracts **service tickets** and cracks them offline to obtain service account passwords.

### How it Works:
1. Authenticate to Active Directory with any domain user
2. Request service tickets (TGS) for accounts with SPNs (Service Principal Names)
3. Extract the ticket (encrypted with the service account's NTLM hash)
4. Crack the ticket offline using tools like Hashcat or John the Ripper

### Tools:
```powershell
# Impacket
GetUserSPNs.py domain/user:password -dc-ip DC_IP -request

# Rubeus
Rubeus.exe kerberoast

# PowerShell
Get-DomainSPNTicket -OutputFormat hashcat
```

### Prevention:
- Use strong, complex passwords for service accounts (25+ characters)
- Use Group Managed Service Accounts (gMSA)
- Monitor service ticket requests
- Limit accounts with SPNs

---

## 6.13 AS-REP Roasting

### What is AS-REP Roasting?
Targets accounts with **Kerberos pre-authentication disabled**. The attacker can request an AS-REP message and crack it offline.

### How it Works:
1. Find accounts with "Do not require Kerberos preauthentication" enabled
2. Send AS-REQ for those accounts
3. Receive AS-REP containing encrypted data (encrypted with user's password hash)
4. Crack offline using Hashcat or John

### Tools:
```bash
# Impacket
GetNPUsers.py domain/ -usersfile users.txt -dc-ip DC_IP

# Rubeus
Rubeus.exe asreproast

# PowerShell
Get-DomainUser -PreauthNotRequired
```

### Prevention:
- Enable Kerberos pre-authentication for all accounts
- Use strong passwords
- Monitor for AS-REP traffic

---

## 6.14 Domain Enumeration with BloodHound

### What is BloodHound?
**BloodHound** is a tool that uses graph theory to reveal hidden relationships and attack paths in Active Directory.

### Key Features:
- Visualizes attack paths to Domain Admin
- Identifies shortest path to high-value targets
- Discovers excessive permissions and group memberships
- Uses **SharpHound** (data collector) to gather AD information

### What BloodHound Reveals:
- Users with admin access
- Group memberships and nested groups
- Trust relationships between domains
- Session information (who is logged in where)
- ACL (Access Control List) abuse paths
- Kerberoastable accounts

### Usage:
```bash
# Collect data with SharpHound
SharpHound.exe -c All

# Or use Python-based collector
bloodhound-python -d domain.local -u user -p password -dc DC01.domain.local -c All

# Import data into BloodHound GUI for visualization
```

---

## 6.15 Golden & Silver Ticket Attacks

### Golden Ticket Attack:
A **Golden Ticket** is a forged TGT that grants unlimited access to any resource in the domain.

| Aspect | Detail |
|---|---|
| **Requires** | NTLM hash of the **krbtgt** account |
| **Provides** | Complete domain admin access |
| **Persistence** | Valid until krbtgt password is changed (TWICE) |
| **Scope** | Entire domain |

### Tool:
```bash
# Mimikatz
kerberos::golden /user:Administrator /domain:domain.local /sid:S-1-5-21-... /krbtgt:HASH /ptt
```

### Silver Ticket Attack:
A **Silver Ticket** is a forged **service ticket** for a specific service.

| Aspect | Detail |
|---|---|
| **Requires** | NTLM hash of the **service account** |
| **Provides** | Access to a specific service only |
| **Persistence** | Valid for 30 days (default) |
| **Scope** | Single service |

### Comparison:

| Feature | Golden Ticket | Silver Ticket |
|---|---|---|
| **Forged Ticket** | TGT | Service Ticket (TGS) |
| **Required Hash** | krbtgt hash | Service account hash |
| **Scope** | Entire domain | Single service |
| **Communicates with KDC** | Yes | No |
| **Detection** | Harder | Easier (no KDC communication) |

### Prevention:
- Change **krbtgt** password regularly (twice in succession for Golden Tickets)
- Monitor for anomalous Kerberos activity
- Implement least privilege
- Use Protected Users security group

---

## 6.16 Lateral Movement

### What is Lateral Movement?
Moving from one compromised system to another within the network to reach high-value targets.

### Lateral Movement Techniques:

| Technique | Description |
|---|---|
| **Pass the Hash (PtH)** | Use NTLM hash to authenticate without knowing the password |
| **Pass the Ticket (PtT)** | Use stolen Kerberos tickets to authenticate |
| **Overpass the Hash** | Convert NTLM hash to a Kerberos ticket |
| **PsExec** | Remote command execution via SMB |
| **WMI (Windows Management Instrumentation)** | Remote command execution |
| **WinRM** | Windows Remote Management |
| **RDP (Remote Desktop Protocol)** | Remote desktop access |
| **SSH** | Secure Shell for Linux/Unix systems |
| **DCOM** | Distributed Component Object Model |
| **SMB** | File sharing for transferring tools/payloads |

### Lateral Movement Tools:

| Tool | Purpose |
|---|---|
| **Mimikatz** | Credential dumping, pass-the-hash, Golden/Silver tickets |
| **CrackMapExec** | Network-wide lateral movement and credential checking |
| **Impacket** | Collection of Python tools for network protocols |
| **PsExec** | Remote command execution |
| **BloodHound** | Finding attack paths |
| **Rubeus** | Kerberos attacks (Kerberoasting, AS-REP Roasting) |
| **PowerView** | AD enumeration |
| **Evil-WinRM** | WinRM shell |
| **Cobalt Strike** | Red team C2 framework |

### Password Cracking Tools (Referenced from Practicals):

| Tool | Description |
|---|---|
| **Hashcat** | GPU-accelerated password cracking |
| **John the Ripper** | CPU-based password cracking |
| **Cain and Abel** | Windows password recovery (deprecated) |
| **Hydra** | Online brute-force tool |
| **Medusa** | Parallel brute-force login tool |

### Metasploit Framework:
- **Purpose:** Exploitation framework for penetration testing
- **Key components:**
  - **msfconsole** – Main command-line interface
  - **Modules** – Exploits, payloads, auxiliary, encoders, post
  - **Meterpreter** – Advanced post-exploitation payload
- **Basic commands:**
  ```
  search <keyword>     # Search for exploits
  use <module>         # Select a module
  show options         # View module parameters
  set RHOSTS <ip>      # Set target
  set PAYLOAD <name>   # Set payload
  exploit / run        # Execute the exploit
  ```
- **Common targets:** Windows XP (MS08-067), Windows 7 (EternalBlue MS17-010)

---

## MCQ Practice Questions

---

**Q1.** During a penetration test, you discover evidence that an unknown attacker has already compromised the system. What should you do?

A. Continue testing and include it in the final report  
B. Ignore it – it's not in your scope  
**C. Immediately notify the client through the defined communication channel** ✅  
D. Try to identify the attacker yourself

> **Explanation:** Finding evidence of a prior or active compromise is a critical communication trigger requiring immediate notification.

---

**Q2.** Which section of a penetration test report is written for non-technical stakeholders like executives?

**A. Executive Summary** ✅  
B. Technical Findings  
C. Appendices  
D. Methodology Section

> **Explanation:** The Executive Summary provides a high-level overview of findings, business impact, and key recommendations in non-technical language.

---

**Q3.** What is the primary goal of a Golden Ticket attack?

A. Crack service account passwords  
B. Enumerate Active Directory  
**C. Forge a TGT for unlimited domain access** ✅  
D. Perform a denial-of-service attack

> **Explanation:** A Golden Ticket is a forged Ticket Granting Ticket (TGT) that provides complete, unrestricted access to the entire domain.

---

**Q4.** Kerberoasting requires which of the following to be successful?

A. Domain Admin privileges  
**B. Any valid domain user account** ✅  
C. Physical access to the Domain Controller  
D. The krbtgt account hash

> **Explanation:** Kerberoasting only requires a regular domain user account to request service tickets for accounts with SPNs.

---

**Q5.** What must be done to invalidate a Golden Ticket?

A. Disable the admin account  
B. Reset the user's password  
**C. Change the krbtgt password TWICE** ✅  
D. Restart the Domain Controller

> **Explanation:** The krbtgt password must be changed twice because the previous password is cached and can still be used to forge tickets.

---

**Q6.** Which tool uses graph theory to visualize attack paths in Active Directory?

A. Mimikatz  
B. CrackMapExec  
**C. BloodHound** ✅  
D. Rubeus

> **Explanation:** BloodHound uses graph theory and graph databases to reveal hidden relationships and identify the shortest attack paths in AD.

---

**Q7.** What is the CVSS score range for a "Critical" vulnerability?

A. 0.0 – 3.9  
B. 4.0 – 6.9  
C. 7.0 – 8.9  
**D. 9.0 – 10.0** ✅

> **Explanation:** Critical vulnerabilities have a CVSS score of 9.0 to 10.0, indicating severe, immediate risk.

---

**Q8.** AS-REP Roasting targets accounts with which specific configuration?

A. Password Never Expires  
**B. Do not require Kerberos preauthentication** ✅  
C. Account is Locked Out  
D. Account is Disabled

> **Explanation:** AS-REP Roasting exploits accounts where Kerberos pre-authentication is disabled, allowing the attacker to request encrypted data without authentication.

---

**Q9.** "Pass the Hash" lateral movement technique uses:

A. Plaintext passwords  
**B. NTLM hash to authenticate without the password** ✅  
C. Kerberos tickets  
D. SSH keys

> **Explanation:** Pass the Hash (PtH) uses the NTLM hash directly for authentication, bypassing the need to know the actual password.

---

**Q10.** After completing a penetration test, which of the following is a critical post-report activity?

A. Sharing findings on social media  
**B. Cleaning up all tools, test accounts, and backdoors** ✅  
C. Keeping copies of all captured credentials  
D. Publishing the report publicly

> **Explanation:** Post-engagement cleanup is critical – remove all tools, test accounts, backdoors, and securely delete captured sensitive data.

---

**Q11.** Which tool is primarily used for credential dumping and pass-the-hash attacks in Windows environments?

**A. Mimikatz** ✅  
B. Nmap  
C. Nikto  
D. Wireshark

> **Explanation:** Mimikatz is the go-to tool for extracting credentials from Windows memory, performing pass-the-hash, and forging Kerberos tickets.

---

**Q12.** A Silver Ticket differs from a Golden Ticket in that:

A. It provides access to the entire domain  
**B. It provides access to a single specific service** ✅  
C. It requires the krbtgt hash  
D. It is more dangerous

> **Explanation:** A Silver Ticket is a forged service ticket that provides access to a specific service only, unlike the Golden Ticket which provides domain-wide access.

---

**Q13.** Which reporting tool is specifically designed for collaborative penetration test reporting?

**A. Dradis** ✅  
B. Nmap  
C. Metasploit  
D. Wireshark

> **Explanation:** Dradis is a collaborative reporting platform designed specifically for security assessment teams to organize and report findings.

---

**Q14.** What is the purpose of SharpHound in Active Directory pentesting?

A. Exploit Kerberos vulnerabilities  
B. Crack passwords  
**C. Collect Active Directory data for BloodHound analysis** ✅  
D. Perform port scanning

> **Explanation:** SharpHound is the data collection tool (ingestor) for BloodHound, gathering AD information about users, groups, sessions, and permissions.

---

**Q15.** Which Metasploit command is used to search for available exploits?

A. `use`  
B. `set`  
**C. `search`** ✅  
D. `exploit`

> **Explanation:** The `search` command in Metasploit searches the database for exploits, payloads, and modules matching a keyword.

---

**Q16.** Common IoT vulnerabilities include all of the following EXCEPT:

A. Default credentials  
B. Lack of encryption  
C. Hardcoded passwords  
**D. Strong authentication mechanisms** ✅

> **Explanation:** Strong authentication is a security feature, not a vulnerability. IoT devices commonly suffer from weak or absent authentication.

---

**Q17.** Which lateral movement technique involves using stolen Kerberos tickets?

A. Pass the Hash  
**B. Pass the Ticket** ✅  
C. PsExec  
D. WMI

> **Explanation:** Pass the Ticket (PtT) uses stolen or forged Kerberos tickets (TGT or TGS) for lateral movement.

---

**Q18.** When reporting a vulnerability, a "Proof of Concept (PoC)" is:

A. A theoretical description of the vulnerability  
**B. Evidence demonstrating that the vulnerability can be exploited** ✅  
C. A cost estimate for remediation  
D. A legal disclaimer

> **Explanation:** A PoC provides concrete evidence (screenshots, commands, outputs) proving that the vulnerability is exploitable.

---

**Q19.** Which password cracking tool is known for GPU-accelerated cracking?

**A. Hashcat** ✅  
B. John the Ripper  
C. Cain and Abel  
D. Hydra

> **Explanation:** Hashcat is the fastest password cracking tool, leveraging GPU acceleration for high-speed cracking.

---

**Q20.** The Metasploit exploit **MS17-010** (EternalBlue) targets which vulnerability?

A. Apache web server flaw  
**B. Windows SMB vulnerability** ✅  
C. Linux kernel vulnerability  
D. SSH protocol weakness

> **Explanation:** MS17-010 (EternalBlue) exploits a vulnerability in the Windows SMB protocol (port 445), notably used in the WannaCry ransomware attack.

---

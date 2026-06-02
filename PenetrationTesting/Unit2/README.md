# Unit 2: Footprinting and Gathering Intelligence

---

## 2.1 Discovering a Target

**Footprinting** (also called **Reconnaissance**) is the first step in gathering information about a target. It involves collecting as much data as possible about the target organization, network, systems, and people.

### Types of Reconnaissance:

| Type | Description | Example |
|---|---|---|
| **Passive Reconnaissance** | Gathering information WITHOUT directly interacting with the target | WHOIS lookup, Google Dorking, social media analysis |
| **Active Reconnaissance** | Directly interacting with the target to gather information | Port scanning, ping sweeps, banner grabbing |

---

## 2.2 Gathering Essential Data

### Information to Gather:
- **Domain names and IP addresses**
- **Email addresses and usernames**
- **Network topology and architecture**
- **Operating systems and services running**
- **Employee names, roles, and contact details**
- **Technologies used (CMS, frameworks, servers)**
- **DNS records (A, MX, NS, CNAME, TXT)**
- **Subdomains**
- **Open ports and services**

---

## 2.3 Website Information Gathering

### Techniques:
- **Viewing page source code** – Reveals HTML comments, hidden fields, scripts
- **Checking robots.txt** – Reveals directories the site doesn't want indexed
- **Analyzing sitemap.xml** – Shows site structure
- **HTTP headers analysis** – Reveals server software, technologies used
- **Cookie analysis** – Reveals session management mechanisms
- **Web archive (Wayback Machine)** – Viewing historical versions of the website
- **CMS identification** – Determining if WordPress, Joomla, Drupal, etc. is used

---

## 2.4 Types of Information Gathering

### 1. Passive Information Gathering
- No direct contact with the target
- Uses publicly available information
- Very low risk of detection
- Examples: Google Dorking, WHOIS, DNS lookups, social media

### 2. Active Information Gathering
- Direct interaction with the target
- Higher risk of detection
- Examples: Port scanning, vulnerability scanning, banner grabbing

### 3. Semi-Passive Information Gathering
- Querying third-party databases that may indirectly contact the target
- Examples: Using Shodan, Censys

---

## 2.5 Open Source Intelligence (OSINT)

**OSINT** is intelligence collected from publicly available sources. It is a critical component of the reconnaissance phase.

### OSINT Sources:

| Category | Sources |
|---|---|
| **Search Engines** | Google, Bing, DuckDuckGo |
| **Social Media** | LinkedIn, Twitter/X, Facebook, Instagram |
| **Public Records** | WHOIS, DNS records, SEC filings |
| **Code Repositories** | GitHub, GitLab, Bitbucket |
| **Job Postings** | Indeed, Glassdoor (reveals technologies used) |
| **Paste Sites** | Pastebin, GitHub Gists |
| **Domain/IP Intelligence** | Shodan, Censys, VirusTotal |
| **Public Databases** | ARIN, RIPE, breach databases |

### Google Dorking (Google Hacking)

**Google Dorking** uses advanced Google search operators to find hidden information, files, and directories on websites.

| Operator | Purpose | Example |
|---|---|---|
| `site:` | Limit results to a specific domain | `site:example.com` |
| `filetype:` | Search for specific file types | `filetype:pdf confidential` |
| `intitle:` | Search in page titles | `intitle:"index of"` |
| `inurl:` | Search in URLs | `inurl:admin` |
| `intext:` | Search in page body text | `intext:"password"` |
| `cache:` | View cached version of a page | `cache:example.com` |
| `link:` | Find pages linking to a URL | `link:example.com` |

> **Key Point:** The purpose of Google Dorking is to **find hidden files and directories on a website**.

---

## 2.6 Human and Physical Vulnerabilities

### Social Engineering

**Social engineering** exploits human psychology to gain unauthorized access. It targets the **weakest link in security — people**.

### Types of Social Engineering Attacks:

| Attack Type | Description |
|---|---|
| **Phishing** | Sending fraudulent emails that appear legitimate to trick users into revealing credentials |
| **Spear Phishing** | Targeted phishing aimed at a specific individual or organization |
| **Whaling** | Phishing targeting high-level executives (CEO, CFO) |
| **Vishing** | Voice phishing – using phone calls |
| **Smishing** | SMS phishing – using text messages |
| **Pretexting** | Creating a fabricated scenario to obtain information |
| **Baiting** | Leaving infected USB drives in public places |
| **Tailgating / Piggybacking** | Following an authorized person into a restricted area |
| **Quid Pro Quo** | Offering something in exchange for information |
| **Dumpster Diving** | Searching through trash for sensitive information |
| **Shoulder Surfing** | Observing someone's screen or keyboard to steal credentials |
| **Watering Hole** | Compromising a website frequently visited by the target |
| **Impersonation** | Pretending to be someone else (e.g., IT support) |

### Physical Attacks:
- **Lock picking** – Gaining physical access through locks
- **Badge cloning** – Duplicating access cards/badges
- **RFID cloning** – Cloning RFID-based access cards
- **Dumpster diving** – Searching trash for sensitive documents
- **Surveillance** – Monitoring physical location
- **USB drop attacks** – Dropping malicious USB devices

---

## 2.7 Key Tools for Information Gathering

### theHarvester
- **Purpose:** Gathers emails, subdomains, hosts, employee names, open ports, and banners from public sources
- **Sources:** Google, Bing, LinkedIn, Shodan, etc.
- **Usage:** `theHarvester -d example.com -b google`

### Recon-ng
- **Purpose:** Full-featured web reconnaissance framework
- **Features:** Modular framework similar to Metasploit, uses modules for different OSINT tasks
- **Key modules:** WHOIS, DNS, contact harvesting, social media
- **Usage:** Interactive console-based tool with marketplace for modules

### Maltego
- **Purpose:** Visual link analysis and data mining tool
- **Features:** Creates visual graphs showing relationships between people, domains, IPs, companies
- **Transforms:** Automated queries that gather and link data
- **Usage:** GUI-based, visual representation of gathered intelligence

### Shodan
- **Purpose:** Search engine for Internet-connected devices
- **Features:** Finds exposed devices (IoT, webcams, servers, industrial systems)
- **Searches for:** Open ports, services, banners, vulnerabilities
- **Usage:** Web-based search or CLI tool
- **Key Point:** Shodan indexes **banners** from services, revealing version info and configurations

### Other Important Tools:

| Tool | Purpose |
|---|---|
| **WHOIS** | Domain registration lookup |
| **nslookup / dig** | DNS query tools |
| **DNSRecon** | DNS enumeration |
| **Sublist3r** | Subdomain enumeration |
| **SpiderFoot** | Automated OSINT collection |
| **FOCA** | Metadata extraction from documents |
| **Metagoofil** | Extracts metadata from public documents |
| **Wayback Machine** | Historical website snapshots |
| **Hunter.io** | Email finding tool |
| **Have I Been Pwned** | Check for breached credentials |

---

## MCQ Practice Questions

---

**Q1.** Which of the following is a method used in search engine analysis for information gathering?

**A. Boolean search operators** ✅  
B. SQL queries  
C. Port scanning  
D. File encryption

> **Explanation:** Boolean search operators (AND, OR, NOT) are used with search engines for advanced information gathering during reconnaissance.

---

**Q2.** What type of data is typically retrieved during OSINT operations from public repositories?

A. Company financial records  
**B. Code vulnerabilities** ✅  
C. User credentials  
D. Malware signatures

> **Explanation:** Public code repositories (GitHub, GitLab) often contain code with vulnerabilities, hardcoded credentials, and configuration files.

---

**Q3.** What is the purpose of using Google Dorking in search engine analysis?

A. To encrypt search results  
B. To index websites faster  
C. To perform denial-of-service attacks  
**D. To find hidden files and directories on a website** ✅

> **Explanation:** Google Dorking uses advanced search operators to discover hidden files, directories, login pages, and sensitive information on websites.

---

**Q4.** Which tool is used for visual link analysis and creating relationship graphs between entities?

A. theHarvester  
B. Recon-ng  
**C. Maltego** ✅  
D. Shodan

> **Explanation:** Maltego specializes in visual link analysis, creating graphs that show relationships between people, domains, IPs, and organizations.

---

**Q5.** A penetration tester is gathering information about a target without directly interacting with the target's systems. What type of reconnaissance is this?

**A. Passive reconnaissance** ✅  
B. Active reconnaissance  
C. Invasive reconnaissance  
D. Dynamic reconnaissance

> **Explanation:** Passive reconnaissance involves gathering information from publicly available sources without directly contacting the target.

---

**Q6.** Which social engineering attack involves sending a targeted phishing email to a specific high-level executive?

A. Phishing  
B. Spear phishing  
**C. Whaling** ✅  
D. Vishing

> **Explanation:** Whaling is a form of spear phishing specifically targeting high-profile individuals like CEOs, CFOs, and other executives.

---

**Q7.** What does Shodan primarily search for?

A. Social media profiles  
B. Email addresses  
**C. Internet-connected devices and their services** ✅  
D. Source code vulnerabilities

> **Explanation:** Shodan is a search engine that indexes Internet-connected devices, revealing open ports, services, banners, and potential vulnerabilities.

---

**Q8.** Which tool would you use to gather email addresses, subdomains, and hosts from public sources?

**A. theHarvester** ✅  
B. Wireshark  
C. Metasploit  
D. John the Ripper

> **Explanation:** theHarvester is specifically designed to collect emails, subdomains, hosts, employee names, and open ports from various public sources.

---

**Q9.** A penetration tester finds a `robots.txt` file on a target website. What can this reveal?

A. User passwords  
B. Database credentials  
**C. Directories the website owner doesn't want indexed by search engines** ✅  
D. The server's operating system

> **Explanation:** The robots.txt file lists directories and pages that should not be crawled by search engines, potentially revealing sensitive areas.

---

**Q10.** Which social engineering technique involves leaving USB drives containing malware in public areas?

A. Tailgating  
B. Pretexting  
**C. Baiting** ✅  
D. Quid pro quo

> **Explanation:** Baiting involves enticing victims with something appealing (like a free USB drive) that contains malware.

---

**Q11.** Which reconnaissance tool is described as a "modular framework similar to Metasploit" for OSINT?

A. Maltego  
**B. Recon-ng** ✅  
C. theHarvester  
D. SpiderFoot

> **Explanation:** Recon-ng is a full-featured reconnaissance framework with a modular design similar to Metasploit.

---

**Q12.** What is the difference between spear phishing and regular phishing?

A. Spear phishing uses phone calls  
**B. Spear phishing targets specific individuals or organizations** ✅  
C. Spear phishing uses SMS messages  
D. There is no difference

> **Explanation:** While regular phishing is sent to many people, spear phishing is targeted at specific individuals or organizations.

---

**Q13.** Which Google Dorking operator would you use to find PDF files on a specific website?

A. `inurl:pdf site:example.com`  
**B. `filetype:pdf site:example.com`** ✅  
C. `intitle:pdf site:example.com`  
D. `cache:pdf site:example.com`

> **Explanation:** The `filetype:` operator searches for specific file types, combined with `site:` to limit to a specific domain.

---

**Q14.** What is "tailgating" in the context of physical security attacks?

A. Following someone's car  
**B. Following an authorized person into a restricted area without authentication** ✅  
C. Stealing someone's badge  
D. Hacking a door lock

> **Explanation:** Tailgating (or piggybacking) is gaining unauthorized physical access by following closely behind an authorized person.

---

**Q15.** Which of the following is NOT an OSINT source?

A. LinkedIn profiles  
B. WHOIS records  
C. GitHub repositories  
**D. Private encrypted databases** ✅

> **Explanation:** OSINT is gathered from publicly available sources. Private encrypted databases are not publicly accessible.

---

**Q16.** During information gathering, a pentester discovers employee email addresses in the format firstname.lastname@company.com. Which tool was most likely used?

**A. theHarvester** ✅  
B. Nmap  
C. Wireshark  
D. Metasploit

> **Explanation:** theHarvester is specifically designed to discover email addresses and their naming conventions from public sources.

---

**Q17.** What is "pretexting" in social engineering?

A. Sending phishing emails  
**B. Creating a fabricated scenario to manipulate a victim into providing information** ✅  
C. Dropping infected USB drives  
D. Shoulder surfing

> **Explanation:** Pretexting involves creating a fake but believable scenario to trick the victim into divulging information.

---

**Q18.** Which technique involves searching through an organization's discarded materials for useful information?

A. Shoulder surfing  
B. Tailgating  
**C. Dumpster diving** ✅  
D. Piggybacking

> **Explanation:** Dumpster diving involves searching through trash and discarded materials for sensitive documents, passwords, or other useful information.

---

**Q19.** What does the `site:` operator do in Google Dorking?

A. Shows the site's source code  
**B. Limits search results to a specific domain** ✅  
C. Finds the site's IP address  
D. Encrypts the search query

> **Explanation:** The `site:` operator restricts Google search results to pages from a specific domain or website.

---

**Q20.** Which of the following is an example of active reconnaissance?

A. Searching LinkedIn for employee names  
B. Looking up WHOIS records  
**C. Performing a port scan on the target** ✅  
D. Reading the company's job postings

> **Explanation:** Port scanning directly interacts with the target system, making it active reconnaissance. All other options are passive.

---

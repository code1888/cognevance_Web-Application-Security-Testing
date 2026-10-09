# 🔐 Web Application Security Testing

**A Level 2 Cybersecurity Project Using Kali Linux, DVWA, Burp Suite, Nikto, and Nmap**

## 👨‍💻 Project Information

- **Project Title:** Web Application Security Testing
- **Submitted By:** Shubham Rajendra Dubele
- **Project Level:** Level 2 — Intermediate
- **Target Application:** DVWA (Damn Vulnerable Web Application)
- **Operating System:** Kali Linux
- **Testing Environment:** Authorized Isolated Laboratory

---

## 📌 1. Project Overview

This project demonstrates a controlled security assessment of a deliberately vulnerable web application in an isolated laboratory environment.

The objective is to identify and understand common web application vulnerabilities, analyze HTTP requests and responses, assess web-server configuration, document security findings, and recommend appropriate mitigation techniques.

The project uses Nmap for service discovery, Nikto for web-server assessment, and Burp Suite for HTTP traffic interception and application testing.

All testing is intended for authorized local laboratory systems only.

## 🎯 2. Objectives

- Set up a controlled web application security testing environment.
- Identify accessible ports and services using Nmap.
- Assess web-server configuration using Nikto.
- Intercept and analyze HTTP requests using Burp Suite.
- Demonstrate SQL Injection in DVWA.
- Demonstrate Cross-Site Scripting (XSS) in DVWA.
- Review HTTP security headers.
- Analyze vulnerability impact and severity.
- Recommend security improvements.
- Prepare technical documentation and a final assessment report.

## 🧪 3. Lab Architecture

```text
             VirtualBox / VMware
                     |
            Isolated Lab Network
                     |
          +----------+----------+
          |                     |
      Kali Linux               DVWA
    Testing Machine         Target Machine
          |                     |
          +------ HTTP ---------+
                     |
             Security Assessment
                     |
          +----------+----------+
          |          |          |
         Nmap      Nikto      Burp Suite
          |          |          |
          +----------+----------+
                     |
             Findings and Report
```

Example IP configuration:

```text
Kali Linux : 192.168.56.10
DVWA       : 192.168.56.20
HTTP Port  : 80
```

**Note:** These IP addresses are examples. Use the actual addresses assigned to your lab machines.

Keep the vulnerable target isolated from public and production networks.

## 🛠️ 4. Tools and Technologies

| Tool | Purpose |
|---|---|
| Kali Linux | Security testing environment |
| DVWA | Intentionally vulnerable target |
| Nmap | Port and service discovery |
| Nikto | Web-server security assessment |
| Burp Suite | HTTP interception and request analysis |
| Firefox | Web application interaction |
| Docker | Optional DVWA deployment |
| VirtualBox / VMware | Virtual laboratory environment |
| Markdown | Technical documentation |

## ⚙️ 5. Installation and Setup

### Step 1: Update Kali Linux

```bash
sudo apt update
```

### Step 2: Install the required tools

```bash
sudo apt install nmap nikto docker.io -y
```

Burp Suite may already be available in Kali. Check by running:

```bash
burpsuite
```

### Step 3: Start Docker

```bash
sudo systemctl enable --now docker
```

### Step 4: Run DVWA

For a local lab where Docker is installed, run the following command:

```bash
sudo docker run --rm -it \
  -p 127.0.0.1:8080:80 \
  vulnerables/web-dvwa
```

Open the application in your browser:

```text
http://127.0.0.1:8080/
```

This example binds the application to the local loopback interface. If you are using a separate DVWA VM, use its lab IP and the appropriate port instead.

### Step 5: Log in to DVWA

The commonly supplied default credentials are:

```text
Username: admin
Password: password
```

If the credentials differ in your deployment, follow the instructions for your DVWA image or installation.

For educational demonstrations, select the appropriate DVWA security level and document the setting used.

## 🔍 6. Testing Methodology

The project follows this workflow:

```text
Target Identification
        |
        v
Nmap Service Discovery
        |
        v
Nikto Web Assessment
        |
        v
Burp Suite HTTP Analysis
        |
        v
SQL Injection Testing
        |
        v
XSS Testing
        |
        v
Evidence Collection
        |
        v
Risk Assessment
        |
        v
Mitigation Recommendations
        |
        v
Final Report
```

## 🔎 7. Nmap Service Discovery

Nmap was used to identify accessible ports and services on the authorized laboratory target.

Basic scan:

```bash
nmap <TARGET-IP>
```

Service detection:

```bash
nmap -sV <TARGET-IP>
```

Create the scan directory:

```bash
mkdir -p scans
```

Save the service scan:

```bash
nmap -sV <TARGET-IP> -oN scans/nmap_service_scan.txt
```

Replace `<TARGET-IP>` with the actual lab target IP. If DVWA is running on localhost, use `127.0.0.1` for the scan.

The output may identify HTTP or other exposed services. Document the actual results obtained from your environment.

## 🛡️ 8. Nikto Web-Server Assessment

Nikto was used to review the authorized web server for potentially risky files, configuration weaknesses, server information, and security-header observations.

Example command for a local DVWA instance:

```bash
nikto -h http://127.0.0.1:8080/
```

Save the results:

```bash
nikto -h http://127.0.0.1:8080/ \
  -output scans/nikto_report.txt
```

For a separate target VM, substitute its actual lab URL.

Nikto findings must be reviewed manually. A scanner warning does not automatically confirm an exploitable vulnerability.

## 🌐 9. Burp Suite HTTP Testing

Burp Suite was used to intercept and inspect HTTP communication between the browser and DVWA.

### Basic procedure

1. Start Burp Suite.
2. Open Proxy settings.
3. Configure the browser to use the Burp proxy.
4. Use a local proxy listener, commonly `127.0.0.1:8080`.
5. Open the DVWA lab application through the browser.
6. Enable interception and inspect the request.
7. Forward the request to the application.
8. Use Repeater to resend authorized test requests when needed.
9. Record relevant request and response observations.

Example request:

```http
GET / HTTP/1.1
Host: 127.0.0.1:8080
User-Agent: Mozilla/5.0
Accept: text/html
```

The actual request may differ depending on the application and browser.

Do not upload session cookies, passwords, authentication tokens, or other sensitive data to GitHub.

## 💉 10. SQL Injection Testing

SQL Injection occurs when user-controlled input changes the intended structure or behavior of a database query because the application does not handle that input safely.

The DVWA SQL Injection module can be used to demonstrate this issue.

Example normal input:

```text
1
```

Controlled laboratory test:

```text
' OR '1'='1
```

Observe whether the application returns unexpected records or behaves differently from the normal input.

### Potential impact

- Unauthorized database queries
- Data disclosure
- Data modification
- Loss of data integrity
- Possible authentication bypass, depending on the application

### Recommended mitigation

- Use parameterized queries and prepared statements.
- Validate input against expected types and formats.
- Apply least-privilege database permissions.
- Avoid exposing detailed database errors.
- Keep database software updated.

**Evidence:** Record the actual test input and result in the project screenshots.

## ⚡ 11. Cross-Site Scripting (XSS) Testing

Cross-Site Scripting occurs when user-controlled content is interpreted as executable browser content.

Use the DVWA XSS module for the controlled demonstration.

Example test payload:

```html
<script>alert('XSS')</script>
```

If the browser executes the JavaScript instead of treating it as ordinary text, the behavior demonstrates XSS in the lab.

### Types of XSS

- **Reflected XSS:** Input is returned in a response and interpreted by the browser.
- **Stored XSS:** Submitted content is stored and later displayed to users.
- **DOM-based XSS:** Client-side JavaScript processes attacker-controlled data unsafely.

### Potential impact

- Page manipulation
- Phishing within a trusted origin
- Unauthorized browser-side actions
- Exposure of browser-side information
- Session compromise, depending on application protections

### Recommended mitigation

- Use context-aware output encoding.
- Validate input appropriately.
- Implement a suitable Content Security Policy (CSP).
- Use safe DOM APIs.
- Configure secure cookie attributes.
- Sanitize HTML only when HTML input is genuinely required.

## 📊 12. Vulnerability Findings

The following table is a sample reporting template. Update the status, severity, and evidence to match your actual test results.

| ID | Finding | Suggested Severity | Evidence |
|---|---|---|---|
| WEB-01 | SQL Injection | High | DVWA SQLi test |
| WEB-02 | Reflected XSS | Medium | DVWA XSS test |
| WEB-03 | Security-header weakness | Low/Medium | HTTP/Nikto output |
| WEB-04 | Information disclosure | Low | Server response |

Severity must be based on exploitability, likelihood, impact, and the application's context. These sample ratings are not confirmed findings for every installation.

Detailed findings are documented in:

```text
findings/vulnerability-findings.md
```

## 📈 13. Risk Assessment

A simple qualitative risk model is:

```text
Risk = Likelihood × Impact
```

| Likelihood | Impact | Indicative Risk |
|---|---|---|
| High | High | Critical/High |
| High | Medium | High |
| Medium | Medium | Medium |
| Low | Low | Low |

Use a consistent scoring methodology when preparing the final report.

## 🛡️ 14. Security Recommendations

### Application security

- Validate user input.
- Use prepared statements for database access.
- Apply context-aware output encoding.
- Avoid unsafe DOM operations.
- Implement appropriate Content Security Policy rules.

### Server security

- Keep server components updated.
- Disable unnecessary services.
- Minimize information disclosure.
- Disable debugging in production.
- Configure security headers according to application requirements.

### Database security

- Apply least privilege.
- Protect database credentials.
- Avoid dynamic SQL construction from untrusted input.
- Use safe error handling.

## 📸 15. Screenshots and Evidence

Store actual screenshots in the `screenshots/` directory.

Recommended screenshots:

```text
01-kali-ip.png
02-dvwa.png
03-nmap.png
04-nikto.png
05-burp-intercept.png
06-burp-repeater.png
07-sqli-input.png
08-sqli-result.png
09-xss-input.png
10-xss-result.png
11-findings.png
```

Only use these filenames after saving the corresponding screenshots. Do not present placeholder images as completed test evidence.

## 📁 16. Project Structure

```text
web-security-project/
│
├── README.md
│
├── docs/
│   ├── methodology.md
│   ├── burp-suite.md
│   ├── nikto.md
│   ├── sql-injection.md
│   └── xss.md
│
├── findings/
│   └── vulnerability-findings.md
│
├── reports/
│   └── security-assessment-report.pdf
│
├── scans/
│   ├── nmap.txt
│   ├── nmap_service_scan.txt
│   └── nikto_report.txt
│
└── screenshots/
    ├── 01-kali-ip.png
    ├── 02-dvwa.png
    ├── 03-nmap.png
    ├── 04-nikto.png
    ├── 05-burp-intercept.png
    ├── 06-burp-repeater.png
    ├── 07-sqli-input.png
    ├── 08-sqli-result.png
    ├── 09-xss-input.png
    ├── 10-xss-result.png
    └── 11-findings.png
```

## 📄 17. Final Report

The full report is stored at:

```text
reports/security-assessment-report.pdf
```

It covers the abstract, introduction, objectives, lab setup, testing methodology, tools, SQL Injection, XSS, findings, risk assessment, mitigation, evidence, conclusion, and references.

## 📚 18. References

- OWASP Web Security Testing Guide (WSTG)
- OWASP Top 10 Web Application Security Risks
- PortSwigger Web Security Academy
- Burp Suite documentation
- Nmap documentation
- Nikto documentation
- Damn Vulnerable Web Application (DVWA) project documentation

## ⚠️ 19. Ethical Disclaimer

This project is intended for education and authorized security testing only. All tests must be performed against systems that you own or have explicit permission to assess.

Keep intentionally vulnerable applications isolated from production and public networks. Do not publish passwords, cookies, tokens, API keys, private data, or unauthorized target information.

## 👨‍💻 Author

**Shubham Rajendra Dubele**

**Project:** Web Application Security Testing  
**Focus:** Web Security, Vulnerability Assessment, and Security Documentation

---

*This project demonstrates a controlled web application security assessment and emphasizes responsible testing, accurate evidence collection, and practical security remediation.*

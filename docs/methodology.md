# 🔐 Security Testing Methodology

## Project Information

**Project:** Web Application Security Testing
**Target:** DVWA
**Environment:** Authorized Isolated Laboratory

## Methodology

The assessment followed a structured web application security testing process.

```text
Target Identification
        ↓
Service Discovery
        ↓
Web Server Assessment
        ↓
HTTP Traffic Analysis
        ↓
Vulnerability Testing
        ↓
Evidence Collection
        ↓
Risk Assessment
        ↓
Mitigation Recommendations
```

## 1. Target Identification

The deliberately vulnerable DVWA application was identified as the authorized target.

## 2. Service Discovery

Nmap was used to identify accessible ports and services.

```bash
nmap -sV <TARGET-IP>
```

## 3. Web Server Assessment

Nikto was used to identify web-server information and potential configuration weaknesses.

```bash
nikto -h http://<TARGET-IP>/
```

## 4. HTTP Analysis

Burp Suite was configured as a local proxy to intercept and analyze HTTP requests and responses.

## 5. Vulnerability Testing

The following vulnerabilities were assessed:

* SQL Injection
* Reflected XSS
* Security-header weaknesses
* Information disclosure

## 6. Evidence Collection

Screenshots and tool outputs were collected and stored in the project repository.

## 7. Risk Assessment

Findings were assessed according to likelihood and potential impact.

## 8. Mitigation

Security recommendations were documented for each finding.

## Ethical Scope

All testing was performed only against the intentionally vulnerable local laboratory target.

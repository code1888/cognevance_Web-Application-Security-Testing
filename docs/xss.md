# ⚡ Cross-Site Scripting (XSS) Testing

## Project Information

**Target:** DVWA
**Environment:** Authorized Isolated Laboratory

## Overview

Cross-Site Scripting (XSS) occurs when attacker-controlled content is interpreted as executable content by a user's browser.

DVWA provides intentionally vulnerable modules for learning and demonstrating XSS.

## Reflected XSS Test

Controlled laboratory payload:

```html
<script>alert('XSS')</script>
```

The test is performed only against the local DVWA application.

## Expected Observation

If the application returns the input without appropriate output encoding and the browser executes the JavaScript, an alert may appear.

## XSS Types

### Reflected XSS

```text
Input
 ↓
HTTP Request
 ↓
Server
 ↓
HTTP Response
 ↓
Browser
```

### Stored XSS

```text
Input
 ↓
Application
 ↓
Database
 ↓
Later Response
 ↓
Browser
```

### DOM-Based XSS

Client-side JavaScript processes attacker-controlled data in an unsafe way.

## Potential Impact

XSS can potentially result in:

* Page manipulation
* Phishing within a trusted origin
* Unauthorized browser-side actions
* Exposure of browser-side information
* Session compromise depending on application protections

## Severity

**Suggested Laboratory Severity: Medium**

Actual severity depends on application context and security controls.

## Evidence

```text
screenshots/09-xss-input.png
screenshots/10-xss-result.png
```

## Mitigation

Recommended protections include:

* Context-aware output encoding
* Input validation
* Content Security Policy (CSP)
* Secure cookie attributes
* Safe DOM APIs
* Appropriate sanitization where HTML input is required

## Secure Data Flow

```text
User Input
    ↓
Validation
    ↓
Context-Aware Encoding
    ↓
Browser
```

## Conclusion

The DVWA XSS module demonstrates why applications must safely handle user-controlled content before placing it into HTML, JavaScript, or other browser-interpreted contexts.

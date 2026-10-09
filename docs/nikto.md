# 🛡️ Nikto Web Server Assessment

## Project Information

**Target:** DVWA
**Environment:** Authorized Isolated Laboratory

## Overview

Nikto is a web-server assessment tool that can identify server information, potentially risky files, configuration observations, and security-header weaknesses.

## Basic Scan

```bash
nikto -h http://<TARGET-IP>/
```

## Save Results

```bash
nikto -h http://<TARGET-IP>/ \
-output scans/nikto_report.txt
```

## Assessment Areas

The assessment considered:

* Server information
* HTTP configuration
* Security headers
* Interesting files
* Directory exposure
* Potentially outdated components

## Evidence

```text
screenshots/04-nikto.png
```

## Output

The scan output is stored at:

```text
scans/nikto_report.txt
```

## Important Note

Nikto findings should be manually reviewed. A scanner observation does not automatically mean that a confirmed exploitable vulnerability exists.

## Recommendations

* Remove unnecessary files
* Disable unnecessary services
* Minimize server information disclosure
* Configure appropriate security headers
* Keep server software updated
* Disable debugging in production

## Conclusion

Nikto provided useful information about the web-server configuration and helped identify areas requiring further security review.

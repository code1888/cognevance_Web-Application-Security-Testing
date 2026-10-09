# 🌐 Burp Suite Testing

## Project Information

**Target:** DVWA
**Environment:** Authorized Isolated Laboratory

## Overview

Burp Suite was used to intercept and analyze HTTP communication between the browser and the DVWA application.

## Proxy Configuration

Typical local proxy configuration:

```text
Proxy Host: 127.0.0.1
Proxy Port: 8080
```

## Testing Procedure

1. Start Burp Suite.
2. Open the Proxy section.
3. Enable interception.
4. Configure the browser to use the Burp proxy.
5. Open the local DVWA application.
6. Observe the intercepted request.
7. Forward the request.
8. Send an authorized request to Repeater when additional analysis is required.

## Example Request

```http
GET / HTTP/1.1
Host: <TARGET-IP>
User-Agent: Mozilla/5.0
Accept: text/html
```

## Repeater

Burp Repeater was used to resend controlled requests and compare application responses.

## Evidence

```text
screenshots/05-burp-intercept.png
screenshots/06-burp-repeater.png
```

## Security Considerations

Session cookies, authentication tokens, passwords, and other sensitive information must be removed or redacted before screenshots are uploaded to GitHub.

## Conclusion

Burp Suite provided visibility into the HTTP communication between the browser and the deliberately vulnerable application and supported controlled application-level testing.

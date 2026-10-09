# 💉 SQL Injection Testing

## Project Information

**Target:** DVWA
**Environment:** Authorized Isolated Laboratory

## Overview

SQL Injection is a web application vulnerability that can occur when user-controlled input is incorporated into database queries without appropriate protection.

DVWA provides an intentionally vulnerable SQL Injection module for educational testing.

## Testing

Normal input:

```text
1
```

Controlled laboratory test:

```text
' OR '1'='1
```

The purpose of this test is to observe whether user input can alter the intended database query behavior.

## Expected Observation

Unexpected records or changes in application behavior may indicate that the input is being incorporated into a database query without sufficient protection.

## Potential Impact

SQL Injection may result in:

* Unauthorized database access
* Data disclosure
* Data modification
* Loss of data integrity
* Authentication bypass in some application designs

## Severity

**Suggested Laboratory Severity: High**

The severity must be reassessed for a real application based on exposure, exploitability, privileges, and business impact.

## Evidence

```text
screenshots/07-sqli-input.png
screenshots/08-sqli-result.png
```

## Mitigation

### Prepared Statements

Use parameterized queries instead of dynamically constructing SQL statements from user input.

### Input Validation

Validate input according to the expected data type and format.

### Least Privilege

The application database account should have only the permissions it requires.

### Safe Error Handling

Avoid exposing database errors and internal implementation details to users.

## Secure Data Flow

```text
User Input
    ↓
Validation
    ↓
Parameterized Query
    ↓
Database
```

## Conclusion

The DVWA SQL Injection module demonstrates the security risks of unsafe database query construction and the importance of parameterized database access.

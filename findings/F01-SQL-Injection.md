# F01 - SQL Injection

**Severity:** Critical

**OWASP Category:** A03 - Injection

**Status:** Confirmed

## Summary

A SQL injection vulnerability was identified in the Juice Shop login functionality. A crafted SQL injection payload supplied through the email parameter bypassed the application's authentication mechanism.

The test payload:

```text
' OR 1=1--
```

resulted in a successful `HTTP/1.1 200 OK` response and authentication as the administrator account.

## Affected Functionality

**Functionality:** User Login

**Endpoint:**

```text
POST /rest/user/login
```

**Affected Parameter:**

```text
email
```

## Description

The application's login functionality is vulnerable to SQL injection because user-controlled input supplied through the email parameter is not being handled safely before being incorporated into a database query.

The injected SQL expression altered the intended authentication query, allowing the authentication condition to evaluate as true.

The successful response demonstrated that the application accepted the malicious input and issued an authentication token for the administrator account.

This indicates that the application is not adequately separating user-supplied data from SQL query logic.

## Methodology

Testing was performed against the locally hosted OWASP Juice Shop instance using Burp Suite Repeater.

### 1. Baseline Test

A normal login request containing invalid credentials was first submitted to establish the expected behaviour.

The application returned:

```text
HTTP/1.1 401 Unauthorized
```

with the response:

```text
Invalid email or password.
```

This established that authentication was functioning normally when invalid credentials were supplied.

### 2. SQL Injection Test

The email parameter was then modified using the following controlled test payload:

```text
' OR 1=1--
```


The modified request was sent through Burp Suite Repeater.

### 3. Validation

The modified request returned:

```text
HTTP/1.1 200 OK
```

The response contained an authentication token and identified the authenticated account as:

```text
admin@juice-sh.op
```

The response data also indicated that the authenticated account had the administrator role.

The difference between the baseline `401 Unauthorized` response and the SQL injection test's `200 OK` response demonstrates a successful authentication bypass.

## Evidence

### Baseline Authentication Failure

The baseline login request returned `401 Unauthorized` with an `Invalid email or password` response.

**File:** ![[login_baseline.png]]

###  SQL Injection Authentication Bypass

The modified login request containing the SQL injection payload returned `200 OK` and authenticated as `admin@juice-sh.op`.

**File:** ![[sqli_authentication_bypass.png]]

Authentication tokens and other token-like values are redacted from public evidence.

## Impact

Successful exploitation allows an attacker to bypass the application's authentication mechanism without knowing the legitimate user's password.

In this test, the vulnerability resulted in authentication as the administrator account. This could provide access to functionality and data intended to be restricted to administrative users.

Potential consequences include:

- Authentication bypass
- Unauthorized access to user accounts
- Unauthorized access to application functionality
- Administrative privilege compromise
- Potential exposure or modification of application data

The demonstrated administrative authentication bypass makes this a critical security issue.

## Remediation

The application should prevent user-controlled input from being interpreted as SQL syntax.

Recommended controls include:

- Use parameterized queries or prepared statements for database operations.
- Do not construct SQL queries through direct string concatenation with user input.
- Use secure database-access abstractions or ORM mechanisms where appropriate.
- Apply server-side input validation as a secondary defensive control.
- Ensure database accounts used by the application follow the principle of least privilege.
- Avoid exposing sensitive authentication data in application responses.
- Implement security testing for injection vulnerabilities as part of the development lifecycle.

Parameterized queries should be the primary control because they separate SQL query structure from user-supplied data.

## OWASP Mapping

**A03 - Injection**

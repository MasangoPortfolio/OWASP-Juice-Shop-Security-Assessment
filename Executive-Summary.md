# Executive Summary

## Assessment Overview

This security assessment was conducted against OWASP Juice Shop `20.2.0`, a deliberately vulnerable web application deployed locally in a controlled testing environment.

The assessment began with environment preparation and verification, followed by reconnaissance of the application's authentication and user-facing functionality. Burp Suite Community Edition was used to intercept, inspect, and replay HTTP requests during testing.

Testing has currently focused on SQL injection within the application's login functionality.

## Work Completed

The following activities have been completed:

- Deployed OWASP Juice Shop `20.2.0` locally.
- Verified that the application was accessible through `127.0.0.1:3000`.
- Configured Burp Suite to intercept application traffic.
- Confirmed that Juice Shop requests appeared in Burp HTTP history.
- Captured and replayed application requests using Burp Repeater.
- Performed reconnaissance of key application functionality, including authentication.
- Established a baseline login response using invalid credentials.
- Tested the login functionality for SQL injection using a controlled payload.
- Successfully demonstrated an authentication bypass through SQL injection.
- Confirmed that the bypass resulted in authentication as the administrator account.
- Collected and sanitised evidence for the confirmed vulnerability.
    

## Current Finding

One vulnerability has been validated at this stage:

| Finding                                   | Severity | Status    |
| ----------------------------------------- | -------- | --------- |
| F01 - SQL Injection Authentication Bypass | Critical | Confirmed |

The SQL injection test against `POST /rest/user/login` resulted in an `HTTP 200 OK` response and authentication as `admin@juice-sh.op`, demonstrating that the application's authentication mechanism can be bypassed through crafted input.

Further testing of Broken Access Control / IDOR and Cross-Site Scripting (XSS) remains outstanding.

## Overall Assessment Status

The assessment is **in progress**. The current results demonstrate that the application contains a critical authentication-related injection vulnerability, while additional testing is required to determine the full security posture of the application.

Severity ratings for future findings will be assigned only after those vulnerabilities have been successfully validated and their impact demonstrated.
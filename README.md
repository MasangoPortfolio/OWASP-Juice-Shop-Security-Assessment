# OWASP Juice Shop Security Assessment

A hands-on web application security assessment of **OWASP Juice Shop 20.2.0**, conducted against a locally hosted instance using **Burp Suite Community Edition**.

The assessment focuses on vulnerability discovery, manual validation, evidence collection, impact assessment, and remediation recommendations.

## Scope

Testing was performed exclusively against a locally hosted instance of OWASP Juice Shop.

**Target:** `http://127.0.0.1:3000`

The assessment covers three vulnerabilities:

| Finding                               | Severity    | Status    |
| ------------------------------------- | ----------- | --------- |
| SQL Injection - Authentication Bypass | Unknown    | Not Confirmed |
| Broken Access Control / IDOR          | Unknown        | Not Confirmed |
| Cross-Site Scripting (XSS)            | Unknown | Not Confirmed |

## Methodology

The assessment followed a structured workflow:

**Environment Setup → Reconnaissance → Vulnerability Discovery → Validation → Impact Assessment → Remediation**

Testing was performed manually using Burp Suite to intercept, inspect, modify, and resend HTTP requests.

## Tools

* **Burp Suite Community Edition** :HTTP interception, request analysis and manipulation
* **Microsoft Edge** : Web application interaction
* **Browser Developer Tools** : Client-side inspection
* **OWASP Juice Shop 20.2.0** : Intentionally vulnerable web application
* **Git / GitHub** : Version control and documentation

## Assessment Structure

| Section                                                     | Description                                           |
| ----------------------------------------------------------- | ----------------------------------------------------- |
| [01 - Environment Setup](01-Environment-Setup.md)           | Local deployment and Burp Suite configuration         |
| [02 - Methodology](02-Methodology.md)                       | Assessment approach and testing methodology           |
| [F01 - SQL Injection](F01-SQL-Injection.md)                 | Authentication bypass through SQL injection           |
| [F02 - Broken Access Control](F02-Broken-Access-Control.md) | IDOR through manipulation of basket identifiers       |
| [F03 - Cross-Site Scripting](F03-XSS.md)                    | XSS through the application search functionality      |
| [Executive Summary](Executive-Summary.md)                   | Summary of findings, impact and recommendations       |
| [Lessons Learned](Lessons-Learned.md)                       | Personal observations and lessons from the assessment |

## Environment

* **OS:** Windows 11 Home Single Language
* **Node.js:** `v24.20.0`
* **npm:** `v11.19.0`
* **Browser:** Microsoft Edge
* **Burp Suite:** `2026.0.7.0.3`
* **Juice Shop:** `20.2.0`
* **Deployment:** Local

## Evidence

Screenshots and supporting evidence are stored in the [`evidence`](evidence/) directory and referenced throughout the individual findings.

Evidence is limited to the information necessary to demonstrate vulnerability discovery and successful validation.

## Disclaimer

This assessment was conducted exclusively against a locally hosted instance of OWASP Juice Shop in a controlled environment. No unauthorised systems or third-party applications were tested.

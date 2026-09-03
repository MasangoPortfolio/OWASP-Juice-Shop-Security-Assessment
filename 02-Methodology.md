# 02 - Methodology

## Assessment Approach

This assessment follows a structured web application security testing process designed to identify, validate, and document security vulnerabilities within OWASP Juice Shop.

The assessment workflow is:

**Reconnaissance → Vulnerability Discovery → Validation → Impact Assessment → Remediation**

Testing is performed manually, with Burp Suite Community Edition used to intercept, inspect, modify, and replay HTTP requests where appropriate.

The assessment environment and initial configuration are documented separately in ([[01-Environment-Setup]])

## 1. Reconnaissance

The application is explored through normal user interactions before exploitation is attempted.

The following functionality is reviewed:

- Authentication and login
- User registration
- Product search
- Product reviews
- Shopping basket
- User account functionality

Burp Suite HTTP history is used to identify relevant endpoints, HTTP methods, parameters, and application responses.

The purpose of reconnaissance is to understand how the application handles user input, authentication, and user-specific resources before testing those areas for vulnerabilities.

## 2. Vulnerability Discovery

Testing will focus on three vulnerability classes selected for investigation:

- SQL Injection
- Broken Access Control / Insecure Direct Object Reference (IDOR)
- Cross-Site Scripting (XSS)
    

Testing will target user-controlled input, authentication functionality, and object identifiers identified during reconnaissance.

At this stage, findings are considered **unverified**. No severity rating is assumed before testing is completed.

## 3. Vulnerability Validation

Potential vulnerabilities will be manually validated using controlled test cases.

Where appropriate, Burp Suite Repeater will be used to:

1. Capture a legitimate request.
2. Establish a baseline response.
3. Modify the relevant parameter or request component.
4. Replay the modified request.
5. Compare the resulting response with the baseline.
6. Determine whether the observed behaviour demonstrates a vulnerability.

A vulnerability will be considered confirmed only when the behaviour can be reproduced and its security impact can be demonstrated

## 4. Impact Assessment

For each confirmed vulnerability, the assessment will consider:

- What an attacker could achieve
- What data or functionality could be affected
- Whether authentication or authorization could be bypassed
- Potential effects on confidentiality, integrity, or availability
- Conditions required for exploitation
    

Severity will be assigned after validation based on the demonstrated impact and exploitability rather than being assumed in advance.

## 5. Remediation

Each confirmed finding will include recommendations addressing the underlying security weakness.

Recommendations will focus on appropriate secure development practices, such as:

- Parameterized queries and prepared statements
- Server-side authorization and ownership checks
- Context-appropriate output encoding
- Secure handling and validation of user-controlled input
- Defense-in-depth controls where appropriate

## Evidence

Evidence will be collected throughout the assessment to support vulnerability validation.

Evidence will focus on the minimum information necessary to demonstrate:

- The relevant functionality
- The baseline request or behaviour
- The test or modified request
- The resulting application behaviour or response
    
Sensitive information such as session tokens, cookies, or unnecessary personal information will be excluded or redacted where applicable.

## Assessment Status

Findings remain **Not Tested** or **Unverified** until the relevant testing has been completed.

Severity ratings and confirmation status will be updated only after sufficient evidence has been collected and the security impact has been demonstrated.
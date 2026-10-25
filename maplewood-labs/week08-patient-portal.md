# Week 8: Patient Portal Login Page Behaving Strangely
**Course:** CPSC 4584 | Special Topics in Information Security
**Date:** October 19, 2026
**Analyst:** Matthew Hansen
**Case ID:** WEB-2026-1019-001

---

## Incident Summary

Patient reports of unexpected behavior on the Maplewood patient portal triggered an SOC investigation. The review found four critical deployment-level security flaws in the login workflow credential exposure via URL parameters, weak session cookie attributes, missing security response headers, and unvalidated post-login redirects.

---

## HTTP Vulnerability Findings

| Finding | Location | Observed Value | Vulnerability | Severity |
|---------|----------|----------------|---------------|----------|
| 1 | Login request method | GET /login?username=jsmith&password=Summer2026 | Credential Exposure in URL | High |
| 2 | Set-Cookie header | Set-Cookie: sessionid=a3f8c2d1; Path=/ | Missing HttpOnly and Secure Attributes | High |
| 3 | Response headers | No HSTS, Content-Security-Policy, or X-Frame-Options | Missing Security Headers | Medium |
| 4 | Redirect handling | next=https://external-site.com/collect | Unvalidated Redirect | High |

---

## Analysis Summary

**Finding 1:** [State the evidence, impact, and proposed remediation direction.]
**Finding 2:** [State the evidence, impact, and proposed remediation direction.]
**Finding 3:** [State the evidence, impact, and proposed remediation direction.]
**Finding 4:** [State the evidence, impact, and proposed remediation direction.]

---

## HTTP Header Inspection Commands Used

| Command | Purpose |
|---------|---------|
| curl -I https://example.com | Login credentials transmitted via GET query strings logged into plaintext; requires transitioning form submission to POST over HTTPS |
| curl -I + grep security headers | Session cookies lack critical hardening flags; HttpOnly, Secure, and SameSite attributes must be enforced to prevent token hijacking |
| curl -v + grep request/response | Shows complete absence of defensive headers leaves clients exposed to script injection; standard hardening headers must be deployed |
| curl -IL + grep HTTP/Location | Unvalidated redirect parameters allow post-auth phishing workflows; server-side domain whitelisting is required to restrict destination targets |

---

## Escalation Summary

Incident WEB-2026-1019-001 at Maplewood Health System: highlights four critical vulnerabilities within the patient portal login workflow that have been documented and escalated.

## Current Findings

Finding 1 (High Severity): The login form utilizes the GET method GET /login?username=jsmith&password=Summer2026!, which exposes plaintext user credentials in server access logs, browser history, and proxy records.   

Finding 2 (High Severity): The session cookie header Set-Cookie: sessionid=a3f8c2d1; Path=/ lacks both HttpOnly and Secure attributes, leaving session tokens vulnerable to Cross-Site Scripting (XSS) theft.

Finding 3 (Medium Severity): The login response completely omits standard security headers Strict-Transport-Security, Content-Security-Policy, and X-Frame-Options, leaving critical browser security controls unenforced.   

Finding 4 (High Severity): Post-authentication redirection accepts external user input next=https://external-site.com/collect | https://external-site.com/collect, creating an unvalidated redirect vulnerability that can be leveraged for sophisticated phishing attacks.

## Next Steps

Fix Login Method: Change the login form from GET to POST so user passwords are no longer exposed in the URL.

Secure Session Cookies: Add HttpOnly, Secure, and SameSite=Strict flags to session cookies to block script access and prevent unencrypted transmission.

Add Security Headers: Turn on standard security headers, including Content-Security-Policy: default-src 'self', to enable built-in browser protections.

Validate Redirects: Restrict post-login redirects using a server-side whitelist so users cannot be routed to untrusted external sites.

As Tier 1 analysts, our scope is limited to observing, documenting, and escalating raw evidence and security implications. Application owners and security engineering teams exclusively handle code modifications, configuration updates, validation testing, and production deployments.

---
*CPSC 4584 | Governors State University | Fall 2026*

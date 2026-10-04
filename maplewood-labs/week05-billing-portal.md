# Week 5: Weak Password Policy Exposes Billing Portal
**Course:** CPSC 4584 | Special Topics in Information Security
**Date:** September 28, 2026
**Analyst:** [Matthew Hansen]
**Incident ID:** INC-2026-0928-001

---

## Incident Summary

An unauthorized remote attacker executed a credential stuffing attack against the Maplewood billing portal, making 847 failed attempts across 12 IP addresses before successfully authenticating to the account billing_admin_03 using the leaked password Maplewood2024!. During the 47-minute unmonitored active session, the attacker accessed sensitive insurance records for 3,247 unique patients.

---

## TLS Assessment

**TLS Version:** TLS 1.3
**Status:** Compliant
**What TLS Protected:** Transport layer security, data integrity, and session confidentiality between client and server in transit.
**What TLS Did Not Protect:** Authentication validity and user authorization, TLS could not detect that valid credentials were presented by an unauthorized attacker.

---

## Authentication Controls Gap Analysis

| Control | Required | Status | Finding |
|---------|----------|--------|---------|
| MFA | Maplewood sensitive-account standard | Not Implemented | Billing accounts relied solely on single-factor password authentication. Enforcing MFA would have blocked the attack after the password was entered. |
| Failed Attempt Protection | Account-based throttling and alerting | Not Implemented | 847 failed login attempts over 72 hours triggered no rate-limiting, account lockout, or SOC alerts. |
| Password Policy | NIST SP 800-63B-4 aligned | Needs Improvement | Password satisfied basic composition length/character rules but allowed organizational context terms Maplewood and failed to screen against known leaked password dictionaries. |
| Compromised Credential Response | Detect and invalidate confirmed compromised authenticators | Not Implemented | Lacked continuous monitoring to cross-reference employee credentials against public breach data, allowing a 6-month-old leaked credential |
| Automated Attack Controls | Throttling, bot detection, or adaptive controls as appropriate | Not Implemented | No IP velocity tracking or behavioral bot detection mechanisms were active to detect and block automated credential stuffing originating from 12 distributed IP addresses. |

---

## OpenSSL Commands Practiced

| Command | Purpose |
|---------|---------|
| openssl genrsa -out private_key.pem 2048 | Generated RSA private key file containing modulus N, public exponent e, private exponent d, and prime factors p and q. |
| openssl rsa -in private_key.pem -pubout | Extracted the public parameters modulus N and public exponent e into public_keypem for distribution. |
| openssl rsa -in private_key.pem -text -noout | Verified internal structure including 2048-bit modulus and primes. |
| cat public_key.pem | Displayed Base64 PEM-encoded public key formatted for X.509 certificate embedding. |

---

## Escalation Summary

Confirmed findings: At 02:14 AM on September 27, 2026, an unauthorized remote attacker successfully authenticated to the billing_admin_03 account using a valid, compromised credential, Maplewood2024!, originating from an overseas IP address. The unauthorized session remained active and unmonitored for 47 minutes before the SOC identified and terminated it. During the session, the attacker accessed insurance and personal health records from over 3,247 unique patients. Authentication log analysis confirmed a total of 847 failed login attempts against the portal across 12 distributed IP addresses over the preceding 72 hours. TLS 1.3 was active and performed as designed to protect transport confidentiality and data integrity, the breach occurred strictly due to application-layer authentication failures.
Key Authentication Gaps: Reliance on single-factor passwords; no MFA enforced on sensitive billing accounts. Lack of failed-attempt throttling, rate-limiting, or automated bot detection. The password policy allowed company terms like Maplewood and failed to screen against known breach lists per NIST SP 800-63B standards. No continuous monitoring to detect and reset compromised credentials leaked online.
Decisions Requiring Leadership Review: Authorize immediate, enterprise-wide MFA enrollment. Include a Formal review of legal and regulatory (HIPAA) patient breach notification protocols. Approval to retain third-party digital forensics to confirm whether data was exfiltrated offsite.

---
*CPSC 4584 | Governors State University | Fall 2026*

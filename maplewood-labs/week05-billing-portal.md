# Week 5: Weak Password Policy Exposes Billing Portal
**Course:** CPSC 4584 | Special Topics in Information Security
**Date:** September 28, 2026
**Analyst:** [Your Name]
**Incident ID:** INC-2026-0928-001

---

## Incident Summary

[One to two sentences describing the credential stuffing attack and what data was accessed.]

---

## TLS Assessment

**TLS Version:** TLS 1.3
**Status:** Compliant
**What TLS Protected:** [Data in transit between client and server]
**What TLS Did Not Protect:** [Authentication -- the attacker had valid credentials]

---

## Authentication Controls Gap Analysis

| Control | Required | Status | Finding |
|---------|----------|--------|---------|
| MFA | Maplewood sensitive-account standard | Not Implemented | [Your finding] |
| Failed Attempt Protection | Account-based throttling and alerting | Not Implemented | [Your finding] |
| Password Policy | NIST SP 800-63B-4 aligned | Needs Improvement | [Your finding] |
| Compromised Credential Response | Detect and invalidate confirmed compromised authenticators | Not Implemented | [Your finding] |
| Automated Attack Controls | Throttling, bot detection, or adaptive controls as appropriate | Not Implemented | [Your finding] |

---

## OpenSSL Commands Practiced

| Command | Purpose |
|---------|---------|
| openssl genrsa -out private_key.pem 2048 | [Explain what this command created.] |
| openssl rsa -in private_key.pem -pubout | [Explain what was derived from the private key.] |
| openssl rsa -in private_key.pem -text -noout | [Explain what key details you inspected.] |
| cat public_key.pem | [Explain what the PEM file contains.] |

---

## Escalation Summary

[Summarize the confirmed findings, the authentication control gaps, and the questions or response decisions that require authorized leadership review.]

---
*CPSC 4584 | Governors State University | Fall 2026*

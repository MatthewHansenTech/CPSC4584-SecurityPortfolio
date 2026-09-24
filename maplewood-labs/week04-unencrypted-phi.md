# Week 4: Unencrypted Patient Records on a Shared Drive
**Course:** CPSC 4584 | Special Topics in Information Security
**Date:** September 21, 2026
**Analyst:** [Matthew Hansen]
**Audit ID:** AUD-2026-0921-001

---

## Incident Summary

We identified an unencrypted shared network folder named "PATIENT_DATA_ARCHIVE" containing 847 files with 8,247 unique patient records exposed to all authenticated network users. Exposed data included patient names, DOBs, SSNs, diagnosis codes, and insurance details, with no historical access logs retained.

---

## HIPAA Compliance Assessment

| Requirement | Status | Finding |
|-------------|--------|---------|
| Encryption at Rest | REQUIRES REVIEW | The current plaintext ePHI was stored on an unencrypted share. Under HIPAA addressable specifications, Maplewood failed to document or implement any equivalent safeguard against unauthorized file access. |
| Access Controls | CONTROL FAILURE | Only read and write permissions were granted across all four clinic locations and inpatient facilities rather than enforcing minimum necessary, role-based access. |
| Audit Controls | CONTROL FAILURE | No historical access logs were retained before discovery, making it impossible to reconstruct previous access or verify whether unauthorized viewing occurred. |

---

## Cryptographic Controls Evaluated

**Base64 encoding:** Evaluated and reclassified as non-protective encoding. Provides no confidentiality because it requires no key and can be reversed with commands like Base64 -d.
**Caesar cipher:** Evaluated as a weak classical cipher. Offers no security because it is vulnerable to brute-force attacks.
**Modern encryption at rest:** Identified as cryptography for collision resistance, which is restricted to legacy file identification only.

---

## Hashing Commands Practiced

| Command | Purpose | Output Length |
|---------|---------|---------------|
| echo -n "..." \| sha256sum | Demonstrated hashing and the avalanche effect when changing a single character | 64 hex characters (256 bits) |
| echo -n "..." \| md5sum | Demonstrated comparison against SHA-256 and highlighted why MD5 is deprecated for collision resistance | 32 hex characters (128 bits) |
| sha256sum .bashrc | Demonstrated establishing a baseline for a system file to detect any unauthorized modifications. | 64 hex characters (256 bits) |

---

## Escalation Summary

The Current Confirmed Findings are that we discovered 847 files containing 8,247 unencrypted patient records stored in plaintext on a clinical shared folder with broad read/write permissions for all authenticated users. High-risk ePHI elements (SSNs, DOBs, medical diagnoses, insurance data) were exposed. Current unknowns include the complete absence of retained historical access logs, it is technically impossible to determine whether unauthorized personnel or external actors accessed, copied, or viewed the ePHI before discovery. The decisions requiring leadership, privacy, security, or legal Review are that authorized executive leadership, legal counsel, and the privacy officer must review these findings to perform a risk assessment under the HIPAA Breach Notification Rule and decide whether mandatory notifications to affected patients are required within the 60-day window. Which as the Tier 1 analyst, I do not make the legal breach determination or select enterprise remediation policies. My job is to create professional documentation and escalate the situation based on the breach.

---
*CPSC 4584 | Governors State University | Fall 2026*

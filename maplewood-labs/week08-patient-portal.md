# Week 8: Patient Portal Login Page Behaving Strangely
**Course:** CPSC 4584 | Special Topics in Information Security
**Date:** October 19, 2026
**Analyst:** Matthew Hansen
**Case ID:** WEB-2026-1019-001

---

## Incident Summary

[One to two sentences describing the patient reports and what the SOC investigation revealed.]

---

## HTTP Vulnerability Findings

| Finding | Location | Observed Value | Vulnerability | Severity |
|---------|----------|----------------|---------------|----------|
| 1 | Login request method | [Record the observed request pattern.] | [Classify the weakness.] | [Your severity assessment] |
| 2 | Set-Cookie header | [Record the missing or present attributes.] | [Classify the weakness.] | [Your severity assessment] |
| 3 | Response headers | [Record the missing protections.] | [Classify the weakness.] | [Your severity assessment] |
| 4 | Redirect handling | [Record how external destination input is handled.] | [Classify the weakness.] | [Your severity assessment] |

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
| curl -I https://example.com | [Explain what response headers you observed.] |
| curl -I + grep security headers | [Explain what your filter returned.] |
| curl -v + grep request/response | [Explain what request and response lines you inspected.] |
| curl -IL + grep HTTP/Location | [Explain what redirect information you observed.] |

---

## Escalation Summary

[Summarize the confirmed findings, their likely security impact, the proposed next steps, and the implementation decisions that belong to authorized application and security personnel.]

---
*CPSC 4584 | Governors State University | Fall 2026*

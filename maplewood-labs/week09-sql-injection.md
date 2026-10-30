# Week 9: SQL Injection Attempt on Appointment Scheduling System
**Course:** CPSC 4584 | Special Topics in Information Security
**Date:** October 26, 2026
**Analyst:** Matthew Hansen
**Case ID:** SQLI-2026-1024-001

---

## Incident Summary

[One to two sentences describing the attack window, the number of log entries, and the escalation from initial probe to targeted PHI extraction.]

---

## SQL Injection Log Analysis

| Entry | Time | Decoded Input | Type | Severity |
|-------|------|---------------|------|----------|
| 1 | 02:14:07 | Johnson | Benign Input | Info |
| 2 | 02:14:52 | ' | Quote Probe | Medium |
| 3 | 02:18:31 | Smith' -- | Comment Syntax Test | High |
| 4 | 02:23:14 | ' OR '1'='1 | Tautology Pattern | High |
| 5 | 02:48:39 | ' UNION SELECT NULL,NULL,NULL -- | UNION Injection Attempt | Critical |
| 6 | 03:01:22 | ' UNION SELECT patient_name,date_of_birth,ssn FROM patients -- | Targeted PHI Extraction Attempt | Critical |

---

## Attack Progression Summary

**Entry 1:** [Explain what this input establishes.]
**Entry 2:** [Explain what this input appears designed to test.]
**Entry 3:** [Explain the role of comment syntax.]
**Entry 4:** [Explain the purpose of the tautology pattern.]
**Entry 5:** [Explain what the UNION pattern may be testing.]
**Entry 6:** [Explain what the targeted column names suggest and what remains unconfirmed.]

---

## Remediation Summary

**Primary application control:** [Explain parameterized queries or prepared statements.]
**Input handling:** [Explain validation for expected format and why it is not a substitute for parameterization.]
**Database permissions:** [Explain least privilege.]
**Detection and monitoring:** [Identify an appropriate logging, alerting, or WAF improvement.]

---

## Escalation Summary

[Summarize the confirmed findings, unresolved question of data return, and the next evidence source required before privacy or legal reviewers can assess disclosure implications.]

---
*CPSC 4584 | Governors State University | Fall 2026*

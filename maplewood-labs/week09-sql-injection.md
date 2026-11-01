# Week 9: SQL Injection Attempt on Appointment Scheduling System
**Course:** CPSC 4584 | Special Topics in Information Security
**Date:** October 26, 2026
**Analyst:** Matthew Hansen
**Case ID:** SQLI-2026-1024-001

---

## Incident Summary

During a 47-minute period, six requests were submitted to the appointment scheduling system. Started with a normal search and gradually escalated into SQL injection attempts, including efforts to test the database and potentially access sensitive patient information.

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

**Entry 1:** Appears as a normal search for the last name Johnson and provides a baseline for regular system activity.
**Entry 2:** The single quote appears to test how the application handles special characters and whether it passes user input directly into a SQL query.
**Entry 3:** Comment syntax is used to ignore the rest of a SQL statement and is often used during SQL injection testing.
**Entry 4:** SQL injection technique that attempts to make a database condition always evaluate as true.
**Entry 5:** The UNION SELECT statement tests whether the application can combine and return data from another query or table.
**Entry 6:** References to patient names, dates of birth, and SSNs suggest an attempt to access sensitive patient information. However, the logs do not confirm that any data was actually returned.

---

## Remediation Summary

**Primary application control:** The application should use parameterized queries or prepared statements so user input is always treated as data and not executable SQL code.
**Input handling:** User input should be validated to ensure it matches expected formats. It's helpful because it uses input validation alongside parameterized queries rather than as a replacement.
**Database permissions:** Least privilege allows access only to the tables and actions required by the application.
**Detection and monitoring:** WE need to enable detailed database logging and configure alerts or a web application firewall (WAF) to detect any suspicious SQL injection patterns.

---

## Escalation Summary

Identified multiple requests that appear consistent with SQL injection testing and attempted data extraction. The most serious request targeted fields with protected patient information. At this time, there is no evidence confirming that patient data was returned or exposed. Review database query logs and related server logs to determine whether any malicious queries executed successfully before legal or privacy teams assess potential disclosure requirements.

---
*CPSC 4584 | Governors State University | Fall 2026*

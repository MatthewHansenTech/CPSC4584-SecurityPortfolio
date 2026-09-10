# Week 2: Suspicious File on a Nurse's Workstation
**Course:** CPSC 4584 | Special Topics in Information Security
**Date:** September 7, 2026
**Analyst:** [Matthew Hansen]
**Incident ID:** INC-2026-0907-001

---

## Incident Summary

At 3:14 AM on September 6, 2026, the Maplewood SOC monitoring system generated an alert for an unexpected file modification located on workstation MHS-C3-NRS-07 in the Clinic 3 outpatient unit. A file named patient_notes.txt appeared in the workstation's home directory and had the execute permission bit set.

---

## Key Findings

**Permission Finding:** The file's permission string is -rwxr--r--, which means the file currently has Read, Write, and Execute permissions for the owner, and Read permissions for the group and others within patient_notes.txt
**File Type Finding:** patient_notes.txt
**Timestamp Finding:** File changed Sep 06 03:14 AM
**Strings Finding:** No readable content was found in patient_notes.txt; we only know the file permission string allows execution.

---

## Terminal Commands Used

| Command | Purpose |
|---------|---------|
| pwd && ls -la | Verifies the current directory path and lists all the files, including their permissions, owners, and size. |
| file [filename] | Provides the true file type, such as ASCII text or its file extension. |
| stat [filename] | Shows detailed data including exact file size and precise timestamps for Modify, Access, Change, and Birth |
| strings [filename] | Prints text to reveal clues like emails and how functions work. |
| find . -mtime -1 -type f | Identifies the files in the current directory that were recently created or modified within 24 hours. |

---

## Escalation Recommendation

I would escalate this situation because we identified that, at the time, no authorized activity was scheduled, which is suspicious. This is especially concerning because the nurse denied placing any files on the workstation during and after her shift, which is strong evidence. Another point is that, while analyzing the document, we see the current permissions are -rwxr--r--, which means the owner made the file executable, even though it should be plain text. We confirmed that no scheduled tasks were configured to create files during overnight hours. The question for the Tier 2 Analyst is: Is the workstation fully compromised, meaning does the attacker have full control of the account, and can we view system logs to track where the suspicious file came from? 

---
*CPSC 4584 | Governors State University | Fall 2026*
    

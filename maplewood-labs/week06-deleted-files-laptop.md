Not Started yet

# Week 6: Deleted Files on a Terminated Employee's Laptop
**Course:** CPSC 4584 | Special Topics in Information Security
**Date:** October 5, 2026
**Analyst:** [Your Name]
**Case ID:** FOR-2026-1005-001

---

## Incident Summary

[One to two sentences describing the termination, the device gap, and the file recovery.]

---

## Chain of Custody Status

**Gap Period:** Oct 3, 2:47 PM to Oct 5, 9:30 AM (approximately 43 hours)
**Gap Significance:** [Your assessment of what the gap means for evidentiary value]
**Documented By:** Analyst on receipt of device

---

## Recovered File Evidence Classification

| Filename | Type | Evidentiary Value | Finding |
|----------|------|-------------------|---------|
| insurance_export_final.xlsx | Spreadsheet | [Your assessment] | [Explain why.] |
| mhs_billing_schema_db.sql | SQL script | [Your assessment] | [Explain why.] |
| vendor_contact_list_external.docx | Document | [Your assessment] | [Explain why.] |
| __tmp_8f2a.dat | Partial artifact | [Your assessment] | [Explain the limitation.] |
| personal_vacation_2025.jpg | Image | [Your assessment] | [Explain why.] |

---

## Metadata Inspection Commands Used

| Command | Purpose |
|---------|---------|
| stat .bashrc | [Explain what metadata you inspected.] |
| ls -lai | [Explain what inode information you observed.] |
| xxd .bashrc \| head -3 | [Explain what the first bytes revealed.] |
| find . -newer .bashrc -type f | [Explain what the time based search returned.] |

---

## Escalation Summary

[Summarize the confirmed technical findings, the custody limitation, and the questions that require authorized legal, HR, or management review.]

---
*CPSC 4584 | Governors State University | Fall 2026*

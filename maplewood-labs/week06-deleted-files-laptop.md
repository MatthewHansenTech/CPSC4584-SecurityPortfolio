# Week 6: Deleted Files on a Terminated Employee's Laptop
**Course:** CPSC 4584 | Special Topics in Information Security
**Date:** October 5, 2026
**Analyst:** Matthew Hansen
**Case ID:** FOR-2026-1005-001

---

## Incident Summary

The termination of billing coordinator Jordan Ellis and an uncoordinated device return created a 43-hour custody gap before we secured the laptop. Our Forensic intake and file carving subsequently recovered five deleted files from unallocated disk space.

---

## Chain of Custody Status

**Gap Period:** Oct 3, 2:47 PM to Oct 5, 9:30 AM (approximately 43 hours)
**Gap Significance:** The 43-hour custody gap reduced confidence in the physical device's integrity and user identity, but operating system logs and file carving confirm verifiable file deletion events within our time window.
**Documented By:** Analyst on receipt of device

---

## Recovered File Evidence Classification

| Filename | Type | Evidentiary Value | Finding |
|----------|------|-------------------|---------|
| insurance_export_final.xlsx | Spreadsheet | High | Was modified at 11:47 PM and deleted just 5 minutes later at 11:52 PM on Oct 3; contains critical exported insurance data removed right after termination. |
| mhs_billing_schema_db.sql | SQL script | High | Represents core billing database structure files deleted at 11:53 PM during the unmonitored custody gap, making it a high-risk data removal artifact |
| vendor_contact_list_external.docx | Document | Medium | Document modified on Oct 2 and deleted at 11:55 PM on Oct 3; relevant to external business relationships but lower sensitivity than core financial/insurance data |
| __tmp_8f2a.dat | Partial artifact | Medium | Only a partial file (22 KB of 400 KB) was recovered from unallocated space; the header was intact, but the content is incomplete, limiting full data reconstruction. |
| personal_vacation_2025.jpg | Image | Low | Deleted at 11:58 PM on Oct 3, but identified as personal non-work photo data, offering minimal evidentiary relevance to corporate misconduct.    |

---

## Metadata Inspection Commands Used

| Command | Purpose |
|---------|---------|
| stat .bashrc | Inspected full file metadata, including Access, Modify, Change, and Birth timestamps to understand file timing and system changes |
| ls -lai |  Observed unique inode numbers, which serve as metadata pointers to file attributes |
| xxd .bashrc \| head -3 | Revealed the ASCII and magic bytes at the file header, demonstrating how carving tools use header/footer signatures to reconstruct files |
| find . -newer .bashrc -type f | A time-based search to isolate files modified within a specific reference window during an investigation |

---

## Escalation Summary

The employee termination on Oct 3 at 2:15 PM followed an unmonitored 43-hour custody gap before the device was returned on Oct 5 at 9:30 AM. Forensic intake included write-blocker application, FTK Imager SHA-256 hash verification, and file carving, which extracted five artifacts from unallocated disk space. Our technical findings confirm that four intact files and one partial data file were deleted between 11:30 PM and 12:04 AM on Oct 3 and Oct 4. While technical evidence proves file presence, modification times, and deletion event timestamps, forensic analysis alone cannot establish intent, authorization status, or someone's user identity. Authorized legal, HR, and management reviewers must evaluate these technical findings alongside independent corroborating evidence.

---
*CPSC 4584 | Governors State University | Fall 2026*

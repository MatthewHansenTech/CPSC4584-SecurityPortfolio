# Week 3: Unauthorized USB Drive in Radiology
**Course:** CPSC 4584 | Special Topics in Information Security
**Date:** September 14, 2026
**Analyst:** Matthew Hansen
**Incident ID:** INC-2026-0914-001

---

## Incident Summary

On September 13, 2026, an unauthorized, unmarked USB drive was discovered plugged into workstation MHS-RAG-WS-03 in a restricted Radiology imaging suite. The device was immediately removed without opening files or mounting the drive, and the workstation has now been isolated from the network
---

## Chain of Custody

Maintaining a chain of custody is essential because it helps ensure evidence integrity, prevent tampering, and preserve evidence for analysis. The evidence was preserved through documented physical transfers from a facilities technician to the IT Helpdesk, to the SOC, and then to us, the Tier 1 analyst, without mounting or executing its contents.
---

## Key Encoding Finding

**String Found:** Y3VybCAtcyAtbyAvZGV2L251bGw=
**Encoding Type:** Base64
**Decoded Content:** curl -s -o /dev/null
**Significance:** The current command silently fetches any content from a server and discards the output to /dev/null to suppress all local traces. The current command lacks a target or URL, meaning further investigation is needed to determine the attacker's intent.

---

## Terminal Commands Used

| Command | Purpose |
|---------|---------|
| echo "..." \| base64 | Demonstrates how plain text is encoded into a Base64 character set which often contains identifiable pattings like having = symbol after a string is encoded. |
| echo "..." \| base64 -d | Decodes the unclear string to reveal the command structure or text |
| xxd .bashrc \| head -6 | Displays byte offsets, with raw hexadecimal byte values, which are used to represent file signatures |
| strings .bashrc \| grep -i "..." | Extracts printable character strings from a binary or script and filters them into a quick isolate potential indicator of compromise. |

---

## Escalation Recommendation

[State whether you would escalate, identify the strongest evidence, and note at least one question that still requires deeper investigation.]
I will escalate this incident to a Tier 2 for deeper investigation. The strongest evidence that supports this escalation is the unauthorized USB drive physically inserted into a workstation with limited overnight network monitoring. Questions include the identity of the person who inserted the drive, whether any commands were executed on the workstation, and what files reside on the USB device.

---
*CPSC 4584 | Governors State University | Fall 2026*

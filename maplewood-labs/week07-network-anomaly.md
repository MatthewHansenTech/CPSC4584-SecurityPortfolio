Not Started

# Week 7: Network Traffic Anomaly During Night Shift
**Course:** CPSC 4584 | Special Topics in Information Security
**Date:** October 12, 2026
**Analyst:** [Your Name]
**Case ID:** NET-2026-1012-001 (related: FOR-2026-1005-001)

---

## Incident Summary

[One to two sentences describing the network anomaly and its connection to the Week 6 disk evidence.]

---

## Network Flow Analysis

| Flow | Source | Destination | Classification | Finding |
|------|--------|-------------|----------------|---------|
| 1 | Webb laptop | 185.220.101.47 | [Your classification] | [State what the flow supports.] |
| 2 | Webb laptop | 185.220.101.47 | [Your classification] | [State why beaconing is or is not supported.] |
| 3 | EHR prod server | AWS | [Your classification] | [Explain why this is baseline or expected traffic.] |
| 4 | Radiology WS | 8.8.8.8 | [Your classification] | [Explain what makes the DNS activity unusual.] |
| 5 | Billing WS | 203.0.113.99 | [Your classification] | [Explain why the nine repeated HTTP connections are consistent with beaconing but not proof of C2.] |

---

## Disk and Network Evidence Correlation

**Disk (Week 6):** [Key timestamps from the disk evidence]
**Network (Week 7):** [Key timestamps from the network evidence]
**Correlation:** [What the combined evidence suggests]
**Limitation:** [What flow data cannot confirm without packet capture]

---

## Network Artifact Inspection Commands Used

| Command | Purpose |
|---------|---------|
| curl -I https://example.com | [Explain what headers you observed.] |
| curl -v --max-time 5 | [Explain what connection and HTTP details were visible.] |
| curl -s -o + xxd | [Explain what the first bytes of the response showed.] |
| curl -s -o /dev/null -w | [Explain which session metrics overlapped with flow concepts.] |

---

## Escalation Summary

[Summarize the confirmed findings, supported correlations, unresolved questions, and the decisions that require authorized incident response or leadership review.]

---
*CPSC 4584 | Governors State University | Fall 2026*

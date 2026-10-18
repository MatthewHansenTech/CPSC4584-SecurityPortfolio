# Week 7: Network Traffic Anomaly During Night Shift
**Course:** CPSC 4584 | Special Topics in Information Security
**Date:** October 12, 2026
**Analyst:** Matthew Hansen
**Case ID:** NET-2026-1012-001 (related: FOR-2026-1005-001)

---

## Incident Summary

Network flow logs show an outbound data transfer from Marcus Webb's laptop matching the size and timing of a deleted insurance spreadsheet from the Week 6 forensic review, along with a consistent beacon-like connection pattern to an external IP address.

---

## Network Flow Analysis

| Flow | Source | Destination | Classification | Finding |
|------|--------|-------------|----------------|---------|
| 1 | Webb laptop | 185.220.101.47 | Suspicious Outbound Transfer | Supports an outbound transfer of 2.4 MB matching the deleted spreadsheet size |
| 2 | Webb laptop | 185.220.101.47 | Potential C2 Beacon | Consistent 312-byte connections every 4 minutes support a beaconing hypothesis, though payload data is lacking |
| 3 | EHR prod server | AWS | Baseline / Expected Traffic | Represents the scheduled nightly EHR backup to the vendor |
| 4 | Radiology WS | 8.8.8.8 | Anomaly / Further Review | Exhibits unusual DNS query volume that warrants a closer look |
| 5 | Billing WS | 203.0.113.99 | Suspicious Periodic Traffic | Nine repeated HTTP connections match a recurring pattern, though not proven C2 |

---

## Disk and Network Evidence Correlation

**Disk (Week 6):** The file INSURANCE_EXPORT_FINAL.XLSX was approximately 2.4 MB, last modified at 11:47 PM, and subsequently deleted at 11:52 PM on October 3.
**Network (Week 7):** Flow 1 recorded an outbound transfer of 2,457,814 bytes from Webb's device 10.4.2.47 to the external IP address 185.220.101.47 beginning at 11:48 PM. Flow 2 captured regular 312-byte connections to the same IP address at four-minute intervals, running from 11:15 PM through 6:42 AM.
**Correlation:** The close alignment in timing and data size between the modified and deleted spreadsheet and Flow 1's outbound transfer supports a sequence where the file was prepped and exfiltrated. The consistent timing and size of Flow 2 establish a beaconing pattern.
**Limitation:** The current network flow records only summarize connection metadata like timestamps, ports, and byte counts and do not contain application payloads; flow data alone cannot definitively prove that the spreadsheet contents were inside that transmission or confirm command-and-control activity without packet captures or corroborating endpoint artifacts

---

## Network Artifact Inspection Commands Used

| Command | Purpose |
|---------|---------|
| curl -I https://example.com |  Retrieved HTTP response headers of HTTP/2 200 OK and Server: Cloudflare without downloading the response body, providing a low-impact header check for server identification |
| curl -v --max-time 5 | Displayed the TLSv1.3 handshake, cipher suite TLS_AES_256_GCM_SHA384, and connection details, showing application-layer telemetry that contrasts with summarized NetFlow records |
| curl -s -o + xxd | The initial bytes of the response are in hex and ASCII formats, displaying readable HTML markup <!doctype html> rather than a fixed binary magic number |
| curl -s -o /dev/null -w | Extracted specific session metrics for the HTTP status code, download size, elapsed time, and remote IP to compare application-session telemetry with traditional network flow fields |

---

## Escalation Summary

Confirmed findings show Webb's laptop generated an outbound transfer of 2,457,814 bytes starting at 11:48 PM, followed by 312-byte connections every four minutes all night. This includes unusual DNS volume on a radiology workstation and recurring HTTP traffic on a billing workstation. Supported Correlations are that Flow 1 matches the size of the deleted insurance spreadsheet and Flow 2 matches beaconing patterns, and the destination IP shares a /24 subnet with a prior credential stuffing incident. Unresolved Questions: Our Flow data alone cannot confirm application payloads, active malware execution, or definitive attribution without deeper endpoint and packet-capture analysis. Authorized Decisions must align with Tier 1 constraints; actions like blocking IPs, changing firewall rules, or making attribution decisions require leadership review rather than independent intervention.

---
*CPSC 4584 | Governors State University | Fall 2026*

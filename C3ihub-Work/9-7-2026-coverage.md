just completed the coverage thing finally and here are the result of it 
before making the final push 



# Detection Scope Matrix: Gap Analysis Report

**Date:** July 2026
**Scope:** Gap analysis of the 50 security capabilities requested in the Detection Scope document against our existing library of 605 Sigma rules.

## Overview
As requested, I have completed the mapping of the 50-item scope document to identify our current detection coverage, identify missing log sources, and highlight requirements that fall outside the scope of our SIEM. 

The attached `detection_coverage_matrix.xlsx` contains the detailed breakdown for every item. Below is a factual summary of the findings.

---

## 1. Summary of Findings

Out of the 50 items requested in the scope document, the analysis breaks down into three main categories:

* **~10 Items (Rule Coverage / Tuning Required):** We have strong coverage for endpoint-focused attacks (e.g., Lateral Movement, WMI abuse). I have also identified a few areas where we have the telemetry but just need to tune or write specific rules (e.g., DCSync, Privilege Escalation).
* **~11 Items (Missing Log Sources):** We currently lack the necessary telemetry to write rules for Cloud Identity and Business Email Compromise (BEC) requirements. 
* **~29 Items (Platform Capabilities):** The remaining items request active prevention, machine learning, or automated response capabilities (e.g., automated ransomware rollback, endpoint DLP blocking, URL rewriting). Because Sigma is an alerting engine, these items represent platform gaps rather than detection rule gaps.

---

## 2. Detailed Gap Breakdown

### A. Data Source Gaps (Missing Telemetry)
For these items, we cannot write detection rules because the SIEM is not receiving the necessary logs. 
* **Cloud Identity:** We currently do not have visibility into Entra ID (Azure AD). Because of this, we cannot detect impossible travel, MFA bypasses, or cloud brute-force attacks.
* **Email Threats:** We cannot detect mailbox forwarding rules created via Web UI/API because O365 Audit logs are not ingested.
* **Network & DNS:** As confirmed by the backend team, we currently only ingest Sysmon Event ID 3 and auditd. This provides basic endpoint connection data, but it is not sufficient for deep network traffic analysis or DNS sinkholing.

**Missing Logs Identified:** Microsoft Entra ID Sign-in & Audit Logs, O365 Unified Audit Log, Email Gateway/Message Trace logs, and DNS Server Analytic logs.

### B. Platform / Capability Gaps (Outside SIEM Scope)
Several requirements in the scope document ask for automated blocking or machine-learning prevention. A SIEM signature engine cannot fulfill these requirements.
* **Endpoint Prevention:** Requirements like pre-execution ML blocking, ransomware rollback, and memory exploit mitigation require an Endpoint Detection and Response (EDR) or Next-Gen AV agent.
* **Web & Email Gateways:** Time-of-click URL rewriting and real-time drive-by download blocking require Secure Web/Email Gateways.
* **Data Security & Cloud:** Blocking USBs/printing based on data labels (Endpoint DLP) and scanning cloud infrastructure for misconfigurations (CSPM) require dedicated enterprise platforms.

### C. Detection Logic Gaps (Actionable Rule Tuning)
For our traditional endpoint and local AD footprint, we have the telemetry and can address these gaps by tuning or writing specific rules:
* **Credential Dumping (DCSync):** We can write a rule for Event ID 4662, filtering on replication GUIDs (`1131f6aa-9c07-11d1-f79f-00c04fc2dcd2`).
* **Privilege Escalation:** We can write rules for `SeDebugPrivilege` assignment (Event 4703) and Linux `sudo` abuse (via `auditd`). *(Note: The 4703 rule will require careful tuning against specific processes to avoid noise).*
* **Agent Tamper Protection:** We can incorporate deterministic service state changes (System Event 7036/7040) to detect security agent tampering.



completed the coverage finally 

now just sharing it to karthik for checking 
even divyanshu verified it all 
and gave feedback that it is fine and i should share it to karthik now 

well karthik called me as he wanted a more deeper coverage and gap data 
cause we lack that 
also he wants me to put data in lack coverage rather than 

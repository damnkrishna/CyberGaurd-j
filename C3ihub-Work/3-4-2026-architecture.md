# C3iHub — Architecture Learning Notes
**Date:** Day 1 / Initial Understanding  
**Context:** Defense Cybersecurity Tool Architecture — Detection & Correlation

---

## 1. Current Architecture Overview

The defense tools being built here are currently working as **standalone detection silos** — meaning each detection system operates independently without talking to the other.

### HIDS Stack
- **Wazuh** — Host-based Intrusion Detection System (HIDS)
- **Sysmon Logs** — Windows endpoint telemetry fed into Wazuh for host-level detection

### NIDS Stack
- **Suricata** — Network Intrusion Detection System (NIDS), using **Proofpoint-bought rules**
- **Zeek** — Network traffic analyzer used alongside Suricata; generates highly structured, formatted logs
- Zeek logs are **stored for manual review** by SOC staff — not yet automated

> **Open Question (still unclear to me):**  
> Are HIDS and NIDS being built as two completely separate tools, or are they one single tool where the connection between the two hasn't been established yet? This needs clarification.

---

## 2. The Core Problem — Siloed Detection

Because HIDS and NIDS are not correlated with each other right now, the detection is happening in isolation:
- A host-level event and a network-level event that are **part of the same attack chain** may never be linked
- SOC staff have to manually analyze Zeek logs without any automated correlation support
- **Defense in depth** is possible on paper — but not being leveraged in practice yet

---

## 3. My Task — Two Parallel Tracks

### Track 1: MITRE ATT&CK — Custom Rule Writing
- Start from the **MITRE ATT&CK Enterprise** database
- Focus on **Reconnaissance techniques** first
- **Prioritize techniques** based on:
  - What the current architecture can actually detect (Wazuh/Sysmon for host, Suricata/Zeek for network)
  - Threat relevance to the deployment context
- Write **custom detection rules** using **Sigma** — the rule language already being used in this setup

### Track 2: Cross-Layer Correlation — Without a Central SIEM
- Think of ways to **correlate HIDS + NIDS logs** for better detection logic
- Goal: write better Sigma rules or detection logic that uses **both host and network signals together**
- Constraint: **No centralized SIEM** to be set up right now — it's out of scope
  - Setting up a central server = big lift
  - Storing long windows of logs for chained attack analysis = requires significant compute/storage capability
  - This is a future problem, not current scope

---

## 4. Why Sigma?

Sigma is the detection rule language already adopted in this stack. The idea is to use Sigma to express detection logic that can work across both HIDS and NIDS layers — or at least write rules that can be applied to each layer's logs individually in a correlated way, without needing a full SIEM pipeline.

---

## Extra — Things to Keep in Mind Going Forward

> *These are additions for future reference — not part of today's direct learning, but relevant context to hold onto.*

- **Sigma rules are backend-agnostic** — the same Sigma rule can be compiled to Wazuh, Splunk, Elastic, etc. This is important when thinking about future SIEM integration.
- **Zeek logs are already structured** (JSON/TSV format with typed fields) — this makes them good candidates for Sigma rule targeting without heavy preprocessing.
- **Chained attack detection** (multi-step attacks like recon → lateral movement) requires a **time-windowed correlation** across log sources — this is the exact gap a SIEM usually fills. Without one, the short-term workaround is writing rules that catch individual steps reliably, then manually connecting the dots.
- **Proofpoint rules in Suricata** cover known signatures — custom rules will need to focus on **behavioral / anomaly-based detection** that those commercial rules don't cover.
- The **prioritization framework** for MITRE techniques should factor in: visibility (can we see it with current stack?), prevalence (is this technique commonly used?), and exploitability (is this likely in the target environment?).

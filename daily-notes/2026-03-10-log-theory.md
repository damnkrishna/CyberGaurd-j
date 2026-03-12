
# 📝 The Logging Cheat Sheet

## 1. The "Big Three" Purposes

* **Observability:** Monitoring health and performance in real-time.
* **Troubleshooting:** Tracing errors (Debugging) and reconstructing timelines (Forensics).
* **Compliance:** Providing an immutable audit trail for legal and security requirements.

---

## 2. Anatomy of a Perfect Log Entry

A log is only as good as its metadata. Use the **** to visualize how these pieces fit together.

| Component | Purpose | Example |
| --- | --- | --- |
| **Timestamp** | Temporal correlation (Use ISO 8601 / UTC). | `2026-03-10T23:30:00Z` |
| **Level** | Severity filtering. | `ERROR`, `WARN`, `INFO` |
| **Source** | Originating service/module. | `payment-gateway` |
| **Event ID** | Unique code for automation/search. | `ERR_402_PAYMENT` |
| **Context** | Structured data (User ID, Request ID). | `{"user_id": 99, "trace_id": "abc"}` |
| **Message** | Human-readable summary. | `Transaction failed: Insufficient funds` |

---

## 3. Log Levels (The Hierarchy)

> 💡 **Pro-Tip:** In production, usually only `INFO` and above are captured to reduce noise and storage costs.

1. **DEBUG:** Granular "behind-the-scenes" info (Dev only).
2. **INFO:** Normal milestones (e.g., "Service started").
3. **WARN:** Non-fatal anomalies (e.g., "High memory usage").
4. **ERROR:** A specific operation failed, but the app lives on.
5. **FATAL/CRITICAL:** The entire system or service is crashing.

---

## 4. Structured vs. Unstructured

* **Unstructured (Bad):** `[10:30] User 5 failed to login.`
* *Problem:* Requires complex Regex to parse; slow for big data.


* **Structured (Good - JSON):** `{"time": "10:30", "user": 5, "status": "fail"}`
* *Benefit:* Instantly searchable by tools like ELK (Elasticsearch) or Splunk.



---

## 5. Do's and Don'ts (The Golden Rules)

### ✅ DO:

* **Use Correlation IDs:** Pass a unique ID across different services to trace a single user request.
* **Automate Rotation:** Ensure logs don't fill up your disk (Logrotate).
* **Centralize:** Send logs to a central server so they aren't lost if a container/server dies.

### ❌ DON'T:

* **Log PII:** Never log passwords, credit card numbers, or Personal Identifying Information (Security risk!).
* **Log too much:** Avoid "Log-orrhea"—if everything is "High Priority," nothing is.
* **Local Time:** Never use local server time; always use **UTC** to sync across global regions.

---
## Types of Logs:

-Application Logs: Messages from specific applications, providing insights into their status, errors, warnings, and other operational details.
-Audit Logs: Events, actions, and changes occurring within a system or application, providing a history of user activities and system behavior.
-Security Logs: Security-related events like logins, permission alterations, firewall activities, and other actions impacting system security.
-Server Logs: System logs, event logs, error logs, and access logs, each offering distinct information about server operations.
-System Logs: Kernel activities, system errors, boot sequences, and hardware status, aiding in diagnosing system issues.
-Network Logs: Communication and activity within a network, capturing information about events, connections, and data transfers.
-Database Logs: Activities within a database system, such as queries performed, actions, and updates.
-Web Server Logs: Requests processed by web servers, including URLs, source IP addresses, request types, response codes, and more.

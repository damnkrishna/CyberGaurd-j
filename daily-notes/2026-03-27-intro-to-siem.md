## Introduction to SIEM

**SIEM** $\Rightarrow$ Security Information and Event Management

### 1) Host-Centric Log Source
Events related to the host:
* User Accessing a file.
* User Attempting to Authenticate.
* Powershell Execution.

### 2) Network-Centric Log Source
Host communicates with each other or accesses the internet to visit websites:
* SSH Connection.
* Web Traffic.
* Network file sharing Activity.

---

### Problems in Log Analysis
* Numerous Log Sources
* No Centralization
* Limited Context
* Limited Analysis
* Format Issues

---

### SIEM Workflow
**SIEM** $\rightarrow$ Collect Data from sources $\rightarrow$ Aggregate Data $\rightarrow$ Discover & Detect Threat $\rightarrow$ Identify Breach & Investigate Alerts

**Key Features:**
* Centralized Log Collection
* Normalization of logs
* Correlation of logs
* Real Time Alerting
* Dashboards & Reporting

---

### Log Ingestion
* Agent / Forwarder
* Syslog
* Manual Upload
* Port-Forwarding

---

### Alert Investigation
Setting up Rules for Detection:

* **Alert is False Positive** $\Rightarrow$ Maybe require tuning the Rule to avoid similar False Positives from occurring again.
* **Alert is True Positive** $\Rightarrow$ Perform further investigation.
    * Contact the asset owner to inquire about the activity.
* **Suspicious Activity is confirmed** $\Rightarrow$ Isolate the infected Host.
* Block the Suspicious IP.

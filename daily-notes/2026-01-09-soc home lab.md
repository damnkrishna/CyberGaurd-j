# 🏠 HOME SOC LAB (8 GB RAM, KALI ONLY)

**Tool:** Wazuh (SIEM + EDR)
**Mode:** Single-node, lightweight, practical

---

## 🔹 PHASE 0 — Mental Model (READ FIRST – 5 min)

Before touching commands, read this so things don’t feel “random”:

### What you’re building

* A **SIEM** → collects logs
* **Rules** → decide what is suspicious
* **Alerts** → notify analyst
* **Dashboard** → analyst visibility
* **Workflow** → how incidents are handled

📘 Read (short):

* What is SIEM: [https://wazuh.com/blog/what-is-siem/](https://wazuh.com/blog/what-is-siem/)
* What does a SOC analyst do: [https://www.splunk.com/en_us/solutions/security-operations-center.html](https://www.splunk.com/en_us/solutions/security-operations-center.html)

Now proceed.

---

## 🔹 PHASE 1 — System Preparation (10 min)

### 1️⃣ Update system

```bash
sudo apt update && sudo apt upgrade -y
```

### 2️⃣ Stop unnecessary services (RAM saving)

```bash
sudo systemctl stop bluetooth
sudo systemctl stop cups
sudo systemctl stop avahi-daemon
```

(Optional: disable permanently)

```bash
sudo systemctl disable bluetooth cups avahi-daemon
```

### 3️⃣ Verify RAM

```bash
free -h
```

✅ You want **Available ≥ 5 GB**

---

## 🔹 PHASE 2 — Install Wazuh (Core SOC) (20–30 min)

### 4️⃣ Install dependencies

```bash
sudo apt install curl apt-transport-https unzip wget -y
```

### 5️⃣ Download Wazuh installation script

```bash
curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh
```

### 6️⃣ Run **single-node installation**

```bash
sudo bash wazuh-install.sh -a
```

⏳ This takes time. Do **nothing else**.

---

### 7️⃣ Save credentials (VERY IMPORTANT)

At the end, you’ll see:

* Dashboard URL
* Username
* Password

📌 **Copy them to a text file NOW**

---

## 🔹 PHASE 3 — Access SOC Dashboard (5 min)

### 8️⃣ Open dashboard

In browser:

```
https://localhost
```

(or IP shown after install)

Accept SSL warning → Login.

✅ If dashboard loads → **SOC is alive**

---

## 🔹 PHASE 4 — Enable Kali as an Agent (10 min)

You will monitor **your own system** (valid SOC practice).

### 9️⃣ Check agent status

```bash
sudo systemctl status wazuh-agent
```

If not running:

```bash
sudo systemctl enable wazuh-agent
sudo systemctl start wazuh-agent
```

### 🔟 Confirm agent in dashboard

* Go to **Endpoints / Agents**
* Status should be **Active**

📘 Read:

* What is an agent: [https://documentation.wazuh.com/current/user-manual/agents/index.html](https://documentation.wazuh.com/current/user-manual/agents/index.html)

---

## 🔹 PHASE 5 — Enable Log Collection (Critical) (15 min)

### 1️⃣ Edit agent config

```bash
sudo nano /var/ossec/etc/ossec.conf
```

Ensure these blocks exist:

#### 🔐 Authentication logs

```xml
<localfile>
  <log_format>syslog</log_format>
  <location>/var/log/auth.log</location>
</localfile>
```

#### 📂 File Integrity Monitoring

```xml
<syscheck>
  <directories>/etc,/bin,/usr/bin</directories>
</syscheck>
```

Save & exit.

### 2️⃣ Restart agent

```bash
sudo systemctl restart wazuh-agent
```

---

## 🔹 PHASE 6 — Generate Security Events (Hands-on) (15 min)

### 🔴 Test 1: Failed Authentication

```bash
su root
# enter wrong password 3–4 times
```

### 🔴 Test 2: Suspicious file creation

```bash
touch /tmp/suspicious_file
```

### 🔴 Test 3: Privilege escalation attempt

```bash
sudo -k
sudo ls
```

---

## 🔹 PHASE 7 — View Logs & Alerts (SOC View) (10 min)

In dashboard:

* Go to **Security Events**
* Filter:

  * `rule.level >= 5`
  * `authentication`
  * `syscheck`

You should see:

* Failed login logs
* File integrity alerts
* Privilege-related logs

📘 Read:

* Wazuh rule levels: [https://documentation.wazuh.com/current/user-manual/ruleset/rules-classification.html](https://documentation.wazuh.com/current/user-manual/ruleset/rules-classification.html)

---

## 🔹 PHASE 8 — Create Custom Alert (SOC Skill) (15 min)

### Create brute-force alert

Edit local rules:

```bash
sudo nano /var/ossec/etc/rules/local_rules.xml
```

Add:

```xml
<rule id="100100" level="10">
  <if_matched_sid>5716</if_matched_sid>
  <description>Possible SSH brute-force attack</description>
  <mitre>T1110</mitre>
</rule>
```

Restart manager:

```bash
sudo systemctl restart wazuh-manager
```

Trigger failed logins again.

🔥 Alert should fire.

---

## 🔹 PHASE 9 — Build Dashboard (10 min)

In Dashboard:

* Go to **Dashboards**
* Create new dashboard
* Add:

  * Authentication failures
  * Alerts by rule level
  * Top users

Keep it simple. SOC dashboards are **boring on purpose**.

---

## 🔹 PHASE 10 — SOC Workflow (MOST IMPORTANT)

Write this in a markdown or text file:

### Incident Report (Example)

```
Alert: SSH Brute Force Detected
Severity: High
Source: Localhost
User Targeted: root
Evidence: Multiple failed authentication attempts
MITRE: T1110
Impact: Potential credential compromise
Action: Recommend account lockout and IP blocking
```

📘 Read:

* MITRE ATT&CK T1110: [https://attack.mitre.org/techniques/T1110/](https://attack.mitre.org/techniques/T1110/)

---

## ✅ FINAL DELIVERABLES (

By end of this:

* ✔ Wazuh running
* ✔ Alerts firing
* ✔ Dashboard created
* ✔ One incident report written





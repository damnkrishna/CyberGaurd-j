# Baseline


## Phase 2: The Baseline Build (Step-by-Step)
Don't try to build a "SOC" yet. Build a **connection**.

### 1. The Manager (The "Ear")
* **Install Ubuntu Server:** Choose the "Minimal" installation. 
* **Static IP:** Research how to set a static IP in Ubuntu. If your Manager's IP changes every time you reboot, your Agents will "go deaf" and won't know where to send logs.
* **Wazuh Installation:** Use the **Wazuh Installation Assistant** (the one-liner command). 
    * **Learning Point:** Read the script output. Don't just wait for it to finish. Watch it install **Elasticsearch** (the database) and **Filebeat** (the log shipper).



### 2. The Agent (The "Voice")
* **Windows VM:** Start with a standard Windows 10/11 VM. 
* **The Handshake:** Download the Wazuh Agent on the Windows machine. When it asks for the "Manager IP," enter the static IP you set in Step 1.
* **Verification:** Go to your Ubuntu Manager’s dashboard (via your laptop's browser). If you see "1 Active Agent," you have officially built a baseline.

---

## Phase 3: The "Understand Everything" Checklist
While building, ask yourself these "Why" questions to actually learn the SOC workflow:

### 1. How do logs move?
* **Check the path:** On your Windows VM, find where the logs live (Event Viewer). 
* **The Experiment:** Close the Wazuh Agent service on Windows. Try to generate an "attack" (like 10 failed logins). Does the Manager see them? (Answer: No). 
* **Lesson:** You learn that visibility is dependent on the health of the **Agent Service**.

### 2. What is a "Rule"?
* **The Logic:** Go into the Wazuh Manager's ruleset (`/var/ossec/ruleset/rules/`). 
* **The Task:** Find the rule for "Successful Windows Login." Look at the XML code. 
* **Lesson:** You’ll see it’s just looking for a specific **Event ID** (like 4624). This is how "magic" detection actually works—it’s just `if/then` statements.

### 3. Networking Basics
* **Firewalls:** If the Agent can't talk to the Manager, check **Port 1514** and **1515**. 
* **Lesson:** You'll learn that in a real company, you have to ask the Network Team to open these specific ports so the SOC can see the data.

---

## Phase 4: The Pivot Point
Once you have **one** Windows machine talking to **one** Ubuntu server, you have reached the "Baseline." 

**Stop there.** Do not add FIM, do not add MITRE, do not add Kali yet. Just make sure that when you create a user on Windows, the Ubuntu server shows an alert within 30 seconds.

**Your First Goal:** * [ ] Ubuntu Server running (No GUI)
* [ ] Windows VM running 
* [ ] Manager/Agent "Active" status in the dashboard.









# to do before ending the project 
## 1. The Architectural Strategy (Manager-Agent)
[cite_start]Your resume claims a "Manager-Agent topology"[cite: 35]. This is the most important technical detail to get right.

* **The Manager (The Brain):** Use **Ubuntu Server** (not Desktop). The "Server" version has no GUI, which saves massive amounts of RAM and CPU—preventing the "hanging" you experienced before.
* [cite_start]**The Agent (The Target):** This is your **Windows 11** VM[cite: 35]. This is where the telemetry (logs) comes from.
* **The Network:** Set both VMs to a **"Host-Only"** or **"Internal Network"** in VirtualBox. This keeps the traffic isolated from your home Wi-Fi but allows the Agent to "talk" to the Manager.


---

## 2. Pre-Flight Checklist (Hardware & BIOS)
To avoid the "fuck ups" from your previous attempt, verify these before installing a single byte:
* **Virtualization:** Ensure **VT-x/AMD-V** is enabled in your ThinkPad BIOS (which you've already done—keep it that way).
* **Resource Allocation:**
    * **Ubuntu Server (Manager):** 2 vCPUs, 4GB RAM (minimum), 20GB Disk.
    * **Windows 11 (Agent):** 2 vCPUs, 4GB RAM, 40GB Disk.
* **Cleanup:** Delete all old, failed VM instances and "vbox" folders to reclaim disk space.

---

## 3. Implementation Checklist: The "Resume-Aligned" Features
To back up the claims in your "Interview Prep" images and resume, you must configure these three specific areas:

### A. File Integrity Monitoring (FIM)
[cite_start]Your resume highlights real-time FIM[cite: 36].
* **The Goal:** Detect when a "hacker" touches a sensitive file.
* **The Task:** In the Wazuh Manager's `ossec.conf`, add the Windows `system32` and `Program Files` directories to the `<syscheck>` section.
* **The Test:** Create or delete a `.txt` file in a monitored folder on Windows and ensure an alert pops up on the Wazuh Dashboard.

### B. MITRE ATT&CK Mapping
You mentioned moving away from "raw log noise" toward "tactic-level attribution".
* **The Task:** Wazuh does much of this automatically, but you must **verify** it. 
* **The Practice:** Trigger a "Pass-the-Hash" or "Brute Force" attack from your Kali VM. Look at the alert in Wazuh and find the **Rule ID** and the **MITRE ID** (e.g., T1078 for Valid Accounts). 
* **The Goal:** Be able to explain *why* an alert is T1543 (Persistence) during an interview.

### C. Telemetry Analysis
* **The Task:** Ensure the Windows Agent is sending more than just "Logins." 
* **The Pro Move:** Install **Sysmon** on your Windows VM. Configure Wazuh to ingest Sysmon logs. This gives you deep visibility into process creations and network connections.

---

## 4. Mental Notes for the "Fresh Start"
* **Discard Kali for Hosting:** As you learned, Kali is for attacking. Use it only as the "External Attacker" sitting outside your SOC network.
* [cite_start]**Documentation is Key:** Since you have a 250+ day GitHub streak[cite: 58], commit your `ossec.conf` files and screenshots of your dashboard alerts. This proves the project is real.
* **Sensitivity vs. Specificity:** Remember your learning about "Alert Fatigue". If your dashboard is flooded with 1,000 alerts in an hour, your "rules" are too sensitive. Part of the project is tuning them down.



# Project started

so finally i started removeed the whole previous model whole previous works and manager and all
now first i am downloading a compatable software for ubuntu vm that has less problem and more stable

so here this tile i am using ubuntu 22.04.5 LTS 

and will try to keep it compatable to this version and my windows laptop 11 home


well i think install will be done this time cause only wazuh-dashboard is giving error this time

so finally my dashboard is up and working but i have to manually put the username and password in wazuh dataset that worked but cause of manually putting password now i have to sync the api too for proper connection too
<img width="1915" height="825" alt="image" src="https://github.com/user-attachments/assets/9dc7ac33-dee8-4dec-8ceb-4a201b9959cc" />



What's next for your SOC Lab?
Now that the server is alive, the fun part starts. You have two choices for your next session:

Option A: Deploy your first Agent. This means installing a tiny piece of software on your Windows 11 host (your actual laptop) so you can see your own security logs show up in Wazuh.

Option B: Log Analysis Practice. Dive into the logs already generated by your Ubuntu VM to see how Wazuh categorizes "Successful Logins" or "Sudo usage."

<img width="959" height="412" alt="image" src="https://github.com/user-attachments/assets/1600278e-9352-4593-9950-a3cee2cbff30" />


fianlly agent deployed too
<img width="797" height="252" alt="image" src="https://github.com/user-attachments/assets/a22a16ae-ceb5-44fc-a1ee-df13b0ca6b9e" />

finally agent connection done i think
i have stop ssl certificate verification i know it should not be done but i had to do it to make it run what can i say

<img width="1906" height="833" alt="image" src="https://github.com/user-attachments/assets/fa6176e8-3b97-4215-a15b-0d2142dd6d59" />
<img width="1916" height="825" alt="image" src="https://github.com/user-attachments/assets/a98efec1-b45b-42ac-981d-40c2f9788813" />
<img width="1919" height="842" alt="image" src="https://github.com/user-attachments/assets/184ad460-dcf3-45c5-8562-e48e166197cd" />


---

## 5. Workflow Summary (The "Paper Trail")
1.  **Attack:** Use Kali to run a Nmap scan or a Hydra brute force against the Windows VM.
2.  **Detect:** The Wazuh Agent picks up the telemetry and sends it to the Ubuntu Manager.
3.  [cite_start]**Alert:** The Manager matches the log against a rule and flags a MITRE ATT&CK technique[cite: 37].
4.  **Analyze:** You open the Wazuh Dashboard, filter by the Windows Agent, and explain what happened.

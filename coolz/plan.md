To get you that deep, granular expertise, we’re going to treat **Phase 1** as the "Data Foundation" phase. If you don't understand how a log is generated, you'll never know if an attacker is tampering with it.

Since you're a visual learner, we will focus on flowcharts and packet/log walkthroughs. Here is your **Day-by-Day "Deep Dive" Plan for Phase 1 (Weeks 1 & 2)**.

-----

## Week 1: The Windows & Linux Anatomy (The Source)

### **Day 1: Windows Event Log Architecture**

  * **Read:** [Microsoft's Windows Event Log Documentation](https://learn.microsoft.com/en-us/windows/win32/wes/windows-event-log) – Focus on the "Channel" and "Provider" concepts.
  * **Watch:** Search YouTube for *"Windows Event Logs for Cyber Security"* (specifically looking for the internal structure of XML logs).
  * **Practice:** Open `eventvwr.msc` on your laptop. Clear your "Security" log. Perform a "Run as Administrator" task. Find the exact Event ID generated (Hint: Look for **4624** or **4688**).

### **Day 2: Sysmon – The SOC Analyst’s Best Friend**

  * **Read:** [SwiftOnSecurity’s Sysmon Config](https://github.com/SwiftOnSecurity/sysmon-config). Read the comments in the XML—they explain *why* certain events are tracked.
  * **Watch:** *"How to Install and Use Sysmon"* by Black Hills Information Security.
  * **Practice:** Install Sysmon on your Windows machine (or a VM). Use the `sysmon -i` command. Open a browser and find the **Event ID 3 (Network Connection)** log it creates.

### **Day 3: Linux Syslog & Journald**

  * **Read:** [DigitalOcean’s Guide to Systemd Logs (journalctl)](https://www.digitalocean.com/community/tutorials/how-to-use-journalctl-to-view-and-manipulate-systemd-logs).
  * **Watch:** Search for *"Linux Logging Explained: /var/log/messages vs Journald"*.
  * **Practice:** On a Linux VM, go to `/var/log/auth.log`. Try to SSH into your own machine with a wrong password 5 times. See how the "Failed password" log looks in raw text.

### **Day 4: Network Protocols (The "Wire")**

  * **Read:** [Cloudflare’s Learning Center on OSI Model](https://www.google.com/search?q=https://www.cloudflare.com/learning/ddos/glossary/osi-model/). Focus on Layer 3 (IP), 4 (TCP/UDP), and 7 (Application).
  * **Watch:** *"TCP Three-Way Handshake Explained"* (Visual animation).
  * **Practice:** Open Wireshark. Filter for `tcp.flags.syn==1`. Visit a website. Watch the SYN-ACK exchange happen in real-time.

### **Day 5: HTTP & DNS Deep Dive**

  * **Read:** [MDN Web Docs on HTTP Messages](https://developer.mozilla.org/en-US/docs/Web/HTTP/Messages).
  * **Watch:** *"How DNS Works"* by Computerphile.
  * **Practice:** Use `nslookup` or `dig` in your terminal. Then, in Wireshark, filter by `dns`. Identify the "Query" and "Response" packets.

-----

## Week 2: Aggregation & Querying (The Visibility)

### **Day 6: Log Transport (The "Pipe")**

  * **Read:** [Logstash vs. Beats vs. Fluentd](https://www.elastic.co/guide/en/beats/libbeat/current/beats-reference.html). Understand how a log gets from a PC to a Server.
  * **Watch:** *"ELK Stack Architecture for Beginners"*.
  * **Practice:** In your Wazuh lab, find the configuration file that tells the agent which logs to send to the manager (`ossec.conf`).

### **Day 7: The SIEM Interface (Kibana/Wazuh Dashboard)**

  * **Read:** [Wazuh Dashboard Documentation](https://documentation.wazuh.com/current/user-manual/wazuh-dashboard/index.html).
  * **Watch:** *"Getting started with Wazuh Dashboard"*.
  * **Practice:** Log into your Wazuh lab. Create a custom filter to only show "Level 10" alerts or higher.

### **Day 8: KQL (Kibana Query Language) Basics**

  * **Read:** [Elastic’s KQL Guide](https://www.google.com/search?q=https://www.elastic.co/guide/en/kibana/current/kuery-query-buttons.html).
  * **Watch:** *"Kibana Query Language (KQL) Tutorial"*.
  * **Practice:** Use KQL to find all logs where `win.eventdata.targetUserName` is your username.

### **Day 9: Regular Expressions (Regex) for Analysts**

  * **Read:** [RegexOne Interactive Lessons](https://regexone.com/).
  * **Watch:** *"Regex in 100 Seconds"*.
  * **Practice:** Go to [Regex102.com](https://regex101.com/). Paste a raw log. Try to write a regex that extracts only the IP address from that log.

### **Day 10: Building a Dashboard**

  * **Read:** [Wazuh Visualizations Guide](https://www.google.com/search?q=https://documentation.wazuh.com/current/user-manual/wazuh-dashboard/visualizations.html).
  * **Watch:** *"Creating Custom Dashboards in Wazuh"*.
  * **Practice:** Create a pie chart in Wazuh that shows the "Top 5 Usernames" attempting to log in to your lab machines.

-----

### **Hardening Your Knowledge (End of Phase 1)**

  * **The Test:** Download a public dataset (like the [BOSSA Nova log samples](https://github.com/logpai/loghub)). Can you tell which log is from a Windows machine and which is from a Cisco router just by looking at the raw text?
  * **The Writing:** Since you like explaining things, write a **1-page summary** (or a blog post on your GitHub) explaining the "Journey of a Log" from a failed login attempt to a dashboard alert.

**Shall we move on to creating the specific "Day-by-Day" plan for Phase 2 (Attack Chains), or do you want to adjust the difficulty of these tasks?**


## **Week 1: The Core Architecture & Data Engine**

### **Day 1: The Splunk Ecosystem & Distributed Search**
*   **Reading:** Splunk Docs: "Inherited Data" and "Distributed Search Overview."
*   **Video:** Search for *"Splunk Architecture: Indexers, Search Heads, and Forwarders explained."*
*   **Practice Question:** If a search is running slowly in a distributed environment, which component (Indexer or Search Head) is responsible for the final aggregation of results?


### **Day 2: Data Life Cycle (The 20% Domain)**
*   **Reading:** **splunk-test-blueprint-cybersecurity-defense-architect.pdf** Section 2.5: Retention, storage tiering, and summarization[cite: 1].
*   **Video:** *"Splunk Data Bucket Lifecycle: Hot, Warm, Cold, Frozen."*
*   **Practice Question:** You need to retain security logs for 365 days for compliance but keep costs low. How do you configure storage tiering to move data after 30 days of inactivity?

### **Day 3: Normalization & The CIM**
*   **Reading:** Section 2.6: The value of data normalization using CIM and CEF[cite: 1].
*   **Video:** *"How to map data to the Splunk Common Information Model (CIM)."*
*   **Practice Question:** You have firewall logs from two different vendors. What is the benefit of using the CIM to map these to the "Network Traffic" data model for a SOC analyst?

### **Day 4: High-Value vs. High-Noise Sources**
*   **Reading:** Section 2.3: Identifying Windows process logs vs. EDR process flows[cite: 1].
*   **Video:** *"Optimizing Splunk Data Ingestion: Reducing License Usage without losing visibility."*
*   **Practice Question:** Why might a Defense Architect prioritize EDR process flow data over standard Windows Event Logs for a malware detection use case?[cite: 1]

### **Day 5: Threat Intelligence Integration**
*   **Reading:** Section 1.0: Developing customized threat intelligence strategies[cite: 1].
*   **Video:** *"Integrating Threat Feeds into Splunk Enterprise Security."*
*   **Practice Question:** Describe the lifecycle of threat intelligence once it is ingested into a broader security operation[cite: 1].

### **Day 6: Advanced Scaling (Data Lakes & Mesh)**
*   **Reading:** Section 2.8: Cybersecurity data architectures using data mesh and federated search[cite: 1].
*   **Video:** *"Splunk Federated Search: Searching across Data Lakes and different Splunk instances."*
*   **Practice Question:** How does Federated Search enable a company to maintain data residency (GDPR) while still allowing a global SOC to hunt for threats?[cite: 1]

### **Day 7: Performance Monitoring & Troubleshooting**
*   **Reading:** Review "Troubleshooting Splunk Enterprise" course objectives from the blueprint[cite: 1].
*   **Video:** *"Using the Splunk Monitoring Console (MC) to find bottlenecks."*
*   **Practice Question:** A user reports that their dashboards are not loading. Using the Monitoring Console, what are the first three metrics you check to diagnose the architecturally-rooted issue?

---

## **The "Architect" Mindset Rules**
1.  **Don't just "learn" the tool:** Always ask *why* a specific architecture (like a multi-site indexer cluster) is better for a business than a single-site one[cite: 1].
2.  **Focus on Section 2.0 and 8.0:** These make up 35% of your exam. They are about how data enters the system and how to choose the right security capabilities[cite: 1].
3.  **Use the "Boss of the SOC" Blogs:** The blueprint recommends these to see how experts actually apply these concepts in a real attack scenario[cite: 1].

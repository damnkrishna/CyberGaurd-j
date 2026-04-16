# 1. How a Log Travels: PC to Server
The process of moving a log from a local PC (the source) to a server (the destination) typically follows these four stages:

1.  **Generation:** An event occurs on the PC (e.g., a failed login or a system error), and the OS or application writes it to a local file.
2.  **Collection:** A "shipper" or "agent" (like Beats or Fluentd) monitors that file for changes.
3.  **Transport:** The shipper sends the log data over the network (usually via encrypted TCP/UDP) to a centralized collector or database.
4.  **Ingestion/Storage:** The server receives the data, parses it, and stores it in a searchable database like Elasticsearch.

---

## 2. Comparing Log Shippers & Processors
While all three tools handle data, they serve different roles within an architecture:

| Tool | Primary Role | Best Used For... |
| :--- | :--- | :--- |
| **Beats** | **Lightweight Shipper** | Low-resource data collection directly from the source (the "PC"). |
| **Logstash** | **Heavyweight Processor** | Complex data transformation, filtering, and routing multiple inputs. |
| **Fluentd** | **Unified Collector** | A flexible, vendor-neutral alternative to Logstash with a massive plugin ecosystem. |



---

## 3. ELK Stack Architecture
The **ELK Stack** (Elasticsearch, Logstash, Kibana) is the industry standard for log management:

* **Logstash/Beats:** Collects and processes the logs.
* **Elasticsearch:** The "brain" that indexes and stores the data for fast searching.
* **Kibana:** The web interface used to create dashboards and visualize the data.

---

## 4. Hands-on: Wazuh Log Configuration
In a security environment like **Wazuh**, the flow is controlled by a specific configuration file on the agent.

* **File Location:** Usually found at `/var/ossec/etc/ossec.conf` (Linux) or `C:\Program Files (x86)\ossec-agent\ossec.conf` (Windows).
* **Key Section:** Look for the `<localfile>` block.
* **The Function:** This block tells the Wazuh agent exactly which file paths to monitor (e.g., `/var/log/auth.log`) and what format they are in. Once defined here, the agent "ships" these logs to the Wazuh Manager (the server).

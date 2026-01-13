# Cybersecurity Detection and Analysis Guide

## Methods of Detection

### Threat Hunting
Proactive security approach where analysts actively search through networks and datasets to detect threats that evade existing automated security solutions. Unlike reactive detection, threat hunting assumes that adversaries are already in the system and works to identify their presence before they cause damage.

### Threat Intelligence
The collection, analysis, and application of information about current and potential cyber threats. This includes understanding threat actors, their tactics, techniques, and procedures (TTPs), and using this knowledge to inform security decisions and strengthen defenses.

### Cyber Deception
Strategic use of decoy systems and false information to mislead attackers and gather intelligence about their methods. The most common implementation is through honeypots.

#### Honeypots
Decoy systems designed to attract attackers and monitor their behavior. These systems appear to be legitimate targets but are actually isolated environments that log attacker activities, providing valuable intelligence without risking production systems.

---

## Common Indicators of Compromise (IoCs) in CI/CD

### Unauthorized Code Changes
Modifications to source code, configuration files, or build scripts that weren't approved through proper change management processes. These changes may indicate an attacker has gained access to the repository or development environment.

### Suspicious Deployment Patterns
Unusual deployment activities such as deployments at odd hours, multiple rapid deployments, or deployments to unexpected environments. These patterns may indicate an attacker attempting to push malicious code into production.

### Compromised Dependencies
Malicious or vulnerable third-party libraries, packages, or containers introduced into the build process. This includes dependency confusion attacks, typosquatting, or legitimate packages that have been compromised.

### Unusual Pipeline Execution
Pipeline jobs running with elevated privileges, executing unexpected commands, or accessing resources outside their normal scope. May also include pipelines triggered by unauthorized users or external sources.

### Secret Exposure Attempts
Activities indicating attempts to extract sensitive credentials, API keys, tokens, or certificates from the CI/CD environment. This includes unusual access to secret management systems or secrets appearing in logs or artifacts.

---

## Indicators of Attack (IoAs)

IoAs focus on the tactics, techniques, and procedures (TTPs) used by attackers rather than specific artifacts left behind. While IoCs tell you *what* happened, IoAs reveal *how* an attack is unfolding in real-time. Examples include:

- **Reconnaissance activities**: Port scanning, enumeration attempts, or information gathering
- **Lateral movement patterns**: Unusual network traffic between systems
- **Privilege escalation attempts**: Multiple failed authentication attempts followed by success
- **Command and control behaviors**: Beaconing patterns or communication with known malicious infrastructure
- **Data staging**: Large amounts of data being compressed or moved to unusual locations

IoAs are more valuable than IoCs because they're harder for attackers to change and can help detect attacks earlier in the kill chain.

---

## Pyramid of Pain

A framework developed by David Bianco that categorizes different types of indicators based on how difficult they are for attackers to change, ranked from easiest (bottom) to hardest (top):

### 1. Hash Values (Trivial)
File hashes (MD5, SHA-1, SHA-256) of malicious files. Easy for attackers to change with minor file modifications.

### 2. IP Addresses (Easy)
Network addresses used by attackers. Relatively simple to change by switching servers or using proxies.

### 3. Domain Names (Simple)
Domains used for command and control or malicious hosting. Inexpensive and quick to register new domains.

### 4. Network/Host Artifacts (Annoying)
Evidence left on systems or networks such as registry keys, file paths, or specific service names. Requires attackers to modify their tools.

### 5. Tools (Challenging)
Specific software or utilities used by attackers. Forces attackers to develop or acquire new tools, requiring time and resources.

### 6. TTPs - Tactics, Techniques, and Procedures (Tough)
The behavioral patterns and methodologies attackers use. Most difficult to change as these represent fundamental approaches to achieving objectives. Forcing attackers to change TTPs significantly increases their operational costs.

The higher you detect on the pyramid, the more "pain" you cause attackers by forcing them to invest more resources into changing their operations.

## Crowdsourcing in Cybersecurity

Leveraging collective intelligence and community contributions to enhance security efforts:

### Threat Intelligence Sharing
Organizations and individuals share information about threats, vulnerabilities, and attack indicators through platforms like ISACs (Information Sharing and Analysis Centers), threat feeds, and collaborative databases.

### Vulnerability Discovery
Bug bounty programs where security researchers are rewarded for finding and reporting vulnerabilities. Platforms like HackerOne, Bugcrowd, and Synack connect organizations with ethical hackers worldwide.

### Security Research Communities
Open-source security projects, forums, and communities (like OWASP, GitHub Security Lab) where researchers collaborate on tools, techniques, and knowledge sharing.

### Benefits
- Diverse perspectives and expertise
- Faster threat detection and response
- Cost-effective security testing
- Global coverage across time zones
- Community-driven innovation

### Challenges
- Quality control and validation
- Coordinating responsible disclosure
- Trust and verification issues


## Report Format
An example of good, structured report following the 5Ws approach

Imagine yourself as an L2 analyst, a DFIR team member, or an IT professional who needs to understand the alert. What would you want to see in the report? We recommend you follow the Five Ws approach and include at least these items in the report:

Who: Which user logs in, runs the command, or downloads the file

What: What exact action or event sequence was performed

When: When exactly did the suspicious activity start and ended

Where: Which device, IP, or website was involved in the alert

Why: The most important W, the reasoning for your final verdict


## Automating task using python 

* Python enables **automation of repetitive cybersecurity tasks**, saving time and reducing human error.
* Used to automate **log collection, parsing, and alerting** from servers, firewalls, and applications.
* Helps in **reconnaissance automation** using APIs and tools for subdomain discovery, OSINT, and scanning.
* Useful for **vulnerability checks** by scripting nmap, HTTP requests, and response analysis.
* Enables **incident response automation** like IOC matching, file hashing, and report generation.
* Integrates easily with **SIEMs, APIs, and security tools** for workflow automation.
* Strong libraries (requests, regex, scapy, pandas) make Python ideal for **security scripting and analysis**.
* almost done

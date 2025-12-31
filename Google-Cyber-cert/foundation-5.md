# Asset Security Threats


## Social Engineering Attacks

Social engineering exploits human psychology rather than technical vulnerabilities to gain unauthorized access to systems, data, or physical locations. These attacks manipulate people into breaking normal security procedures or divulging confidential information.

### Email Phishing
**Email phishing** is the most common form of social engineering attack. Attackers send fraudulent emails that appear to be from legitimate sources (banks, companies, government agencies) to trick recipients into:
- Clicking malicious links
- Downloading infected attachments
- Revealing sensitive information like passwords or credit card numbers

**Key characteristics:** Mass distribution, generic greetings, urgent language, suspicious links or attachments.

### Smishing (SMS Phishing)
**Smishing** uses text messages (SMS) instead of email to conduct phishing attacks. Victims receive text messages containing:
- Fake alerts about account problems
- Prize notifications requiring immediate action
- Links to malicious websites
- Requests to call fraudulent phone numbers

**Common scenarios:** Package delivery notifications, bank security alerts, tax refund messages.

### Vishing (Voice Phishing)
**Vishing** involves phone calls where attackers impersonate legitimate entities to extract sensitive information. Attackers often use:
- Caller ID spoofing to appear legitimate
- Social engineering scripts to build trust
- Urgency and fear tactics to pressure victims
- Voice manipulation technology

**Target information:** Bank account details, social security numbers, login credentials, verification codes.

### Spear Phishing
**Spear phishing** is a targeted attack directed at specific individuals or organizations. Unlike mass phishing campaigns, these attacks:
- Research victims extensively beforehand
- Personalize messages with specific details
- Reference real relationships, projects, or events
- Appear highly credible and relevant

**Success rate:** Significantly higher than generic phishing due to personalization.

### Whaling
**Whaling** targets high-profile executives, senior management, or other "big fish" within organizations. These sophisticated attacks:
- Focus on C-level executives (CEO, CFO, CTO)
- Often impersonate legal, tax, or business communications
- Aim for large financial transfers or sensitive corporate data
- Use advanced social engineering techniques

**Impact:** Potentially catastrophic due to victims' access levels and authority.

### Angler Phishing
**Angler phishing** exploits social media platforms by impersonating customer service accounts. Attackers:
- Monitor social media for customer complaints
- Create fake support accounts mimicking legitimate brands
- Respond to frustrated customers before real support teams
- Direct victims to malicious websites or request credentials

**Platforms:** Twitter, Facebook, Instagram, LinkedIn.

---

## Malware Threats

Malware (malicious software) is designed to infiltrate, damage, or gain unauthorized access to computer systems. Understanding different malware types is essential for implementing effective defense strategies.

### Virus
A **computer virus** is malicious code that attaches itself to legitimate programs or files and replicates when the infected file is executed. Characteristics include:
- Requires user action to spread (opening files, running programs)
- Can corrupt or delete data
- May remain dormant until triggered
- Spreads through infected files, email attachments, or removable media

**Types:** File infector, macro virus, boot sector virus, polymorphic virus.

### Worm
**Worms** are self-replicating malware that spread automatically across networks without human intervention. Key features:
- Exploit network vulnerabilities to propagate
- Consume bandwidth and system resources
- Can spread rapidly across entire networks
- Often used to create botnets or deliver additional payloads

**Famous examples:** Morris Worm, ILOVEYOU, WannaCry, Conficker.

### Trojan (Trojan Horse)
**Trojans** disguise themselves as legitimate software to trick users into installing them. Unlike viruses, they don't self-replicate but:
- Appear as useful applications, updates, or files
- Create backdoors for remote access
- Download additional malware
- Steal sensitive information

**Common types:** Backdoor trojans, banking trojans, downloader trojans, RAT (Remote Access Trojan).

### Ransomware
**Ransomware** encrypts victim's files or locks systems, demanding payment for restoration. This increasingly common threat:
- Encrypts files using strong cryptography
- Displays ransom demands (often in cryptocurrency)
- May threaten to leak sensitive data
- Targets individuals, businesses, and critical infrastructure

**Attack vectors:** Phishing emails, exploit kits, compromised websites, RDP vulnerabilities.

### Spyware
**Spyware** secretly monitors user activity and collects information without consent. Capabilities include:
- Keystroke logging (keyloggers)
- Screen capture
- Tracking browsing habits
- Harvesting credentials and personal data

**Impact:** Identity theft, financial fraud, privacy violations, corporate espionage.

### Adware
**Adware** automatically displays or downloads advertising content. While sometimes legitimate, malicious adware:
- Generates unwanted pop-up advertisements
- Redirects browsers to advertising websites
- Tracks user behavior without permission
- Slows system performance

**Distribution:** Bundled with free software, browser extensions, fake updates.

### Scareware
**Scareware** uses fear tactics to manipulate users into purchasing fake or malicious software. Common tactics:
- Fake security alerts claiming system infections
- Bogus system scans showing numerous threats
- Urgent warnings demanding immediate action
- Pushing victims to buy useless "security" software

**Also known as:** Rogue security software, fake antivirus.

### Rootkit
**Rootkits** provide privileged (root-level) access while hiding their presence from users and security software. Characteristics:
- Operate at kernel or firmware level
- Extremely difficult to detect and remove
- Hide malicious processes, files, and network connections
- Used by attackers to maintain persistent access

**Types:** User-mode, kernel-mode, bootloader, firmware/hardware rootkits.

### Botnet
A **botnet** is a network of compromised computers (bots/zombies) controlled remotely by attackers. Used for:
- Distributed Denial of Service (DDoS) attacks
- Spam email distribution
- Cryptocurrency mining
- Credential stuffing attacks
- Hosting malicious content

**Structure:** Command and Control (C&C) server, bot herders, infected machines.

### Cryptojacking
**Cryptojacking** hijacks computing resources to mine cryptocurrency without the owner's knowledge or consent. Impacts include:
- Increased electricity costs
- Reduced system performance
- Overheating and hardware damage
- Shortened device lifespan

**Methods:** Malicious scripts on websites, infected applications, cloud infrastructure compromise.

---

## Injection Attacks

Injection attacks occur when untrusted data is sent to an interpreter as part of a command or query. These attacks exploit vulnerabilities in applications that fail to properly validate, sanitize, or escape user input.

### Cross-Site Scripting (XSS)
**Cross-Site Scripting (XSS)** allows attackers to inject malicious scripts into web pages viewed by other users. Consequences include:
- Session hijacking through cookie theft
- Credential harvesting
- Website defacement
- Redirecting users to malicious sites
- Delivering malware

#### DOM-Based XSS
**DOM-Based XSS** occurs entirely in the Document Object Model (DOM) without server involvement. The vulnerability exists when:
- Client-side JavaScript processes user input unsafely
- Data flows from source (URL parameters, user input) to sink (dangerous JavaScript functions)
- The attack payload never reaches the server

**Example:** Unsafe use of `document.write()`, `innerHTML`, or `eval()` with user-controlled data.

#### Reflected XSS
**Reflected XSS** (non-persistent) occurs when malicious scripts are reflected off a web server. Characteristics:
- Attack is delivered through a single request/response
- Victim must click a crafted link or submit a malicious form
- Script is not stored on the server
- Often delivered via phishing emails or malicious websites

**Common target:** Search results, error messages, URL parameters.

#### Stored XSS
**Stored XSS** (persistent) is the most dangerous type where malicious scripts are permanently stored on target servers. Features:
- Injected scripts saved in databases, forums, comment fields, etc.
- Executes automatically when victims view the compromised page
- Affects multiple users without additional attacker interaction
- Harder to detect and can persist long-term

**High-risk areas:** User profiles, message boards, comment sections, file upload features.

### SQL Injection
**SQL Injection** exploits vulnerabilities in database queries to execute unauthorized SQL commands. Attackers can:
- Bypass authentication mechanisms
- Extract sensitive database information
- Modify or delete database records
- Execute administrative operations on the database
- Access underlying operating system

#### In-Band SQL Injection
**In-Band SQL Injection** (classic) is the most common and straightforward type where:
- Attack and result retrieval use the same communication channel
- Attacker sees results directly in the application response

**Subtypes:**
- **Error-based:** Forces database to produce error messages revealing structure
- **Union-based:** Uses UNION SQL operator to combine results from multiple queries

#### Out-of-Band SQL Injection
**Out-of-Band SQL Injection** relies on alternative channels to exfiltrate data when in-band techniques aren't possible. Characteristics:
- Uses database server's ability to make DNS or HTTP requests
- Results sent to attacker-controlled server
- Less common due to specific server configuration requirements

**Use cases:** When error messages are suppressed and data can't be retrieved in-band.

#### Inferential SQL Injection (Blind)
**Inferential (Blind) SQL Injection** doesn't directly transfer data but allows attackers to infer information by observing application behavior. Methods:
- **Boolean-based:** Asking true/false questions and observing different responses
- **Time-based:** Using database delay functions to infer information based on response time

**Technique:** Reconstruct database content character by character through systematic queries.

---

## Protection Techniques

### PASTA (Process for Attack Simulation and Threat Analysis)

**PASTA** is a comprehensive, risk-centric threat modeling methodology that aligns business objectives with technical requirements. It provides a structured, seven-stage process for identifying and evaluating threats throughout the software development lifecycle.

#### Overview
PASTA is designed to:
- Bridge the gap between business stakeholders and technical teams
- Provide risk-based analysis focusing on business impact
- Enable proactive security measures during development
- Create actionable remediation strategies

#### The Seven Stages of PASTA

##### Stage 1: Define Objectives
**Purpose:** Establish the business context and security requirements for the threat model.

**Activities:**
- Identify business objectives and security goals
- Define compliance requirements (GDPR, HIPAA, PCI-DSS, etc.)
- Determine scope of the threat model
- Establish risk appetite and acceptance criteria
- Document stakeholder concerns and priorities

**Output:** Clear understanding of what needs protection and why.

##### Stage 2: Define Technical Scope
**Purpose:** Create a comprehensive technical view of the environment under analysis.

**Activities:**
- Document application architecture and infrastructure
- Identify all technology components (databases, APIs, frameworks)
- Map network boundaries and trust zones
- Catalog data flows and integration points
- List third-party dependencies and services

**Output:** Detailed technical architecture diagrams and documentation.

##### Stage 3: Application Decomposition
**Purpose:** Break down the application into analyzable components to understand data flow and trust boundaries.

**Activities:**
- Create Data Flow Diagrams (DFDs)
- Identify entry and exit points
- Document authentication and authorization mechanisms
- Map user roles and privileges
- Analyze session management and data storage

**Output:** Component-level understanding of application structure and behavior.

##### Stage 4: Threat Analysis
**Purpose:** Identify potential threats using structured approaches and threat intelligence.

**Activities:**
- Apply threat frameworks (STRIDE, OWASP Top 10, MITRE ATT&CK)
- Review historical attack patterns and current threat landscape
- Conduct brainstorming sessions with security experts
- Analyze emerging vulnerabilities and exploit trends
- Document threat scenarios specific to the application

**STRIDE Model:**
- **S**poofing identity
- **T**ampering with data
- **R**epudiation
- **I**nformation disclosure
- **D**enial of service
- **E**levation of privilege

**Output:** Comprehensive threat library relevant to the application.

##### Stage 5: Vulnerability and Weakness Analysis
**Purpose:** Identify existing vulnerabilities in the application and infrastructure.

**Activities:**
- Conduct code reviews (static analysis)
- Perform vulnerability scanning
- Review security configurations
- Analyze authentication and cryptographic implementations
- Assess third-party component vulnerabilities
- Examine previous penetration test results

**Output:** Documented vulnerabilities mapped to identified threats.

##### Stage 6: Attack Modeling and Simulation
**Purpose:** Analyze how identified threats could exploit vulnerabilities through attack trees and scenarios.

**Activities:**
- Create attack trees showing potential attack paths
- Simulate attack scenarios
- Assess attack feasibility and likelihood
- Evaluate existing security controls effectiveness
- Identify gaps in security defenses
- Calculate potential attack surface

**Output:** Realistic attack scenarios with probability assessments.

##### Stage 7: Risk and Impact Analysis
**Purpose:** Quantify risks and prioritize remediation efforts based on business impact.

**Activities:**
- Calculate risk scores (likelihood × impact)
- Assess business impact of successful attacks
- Prioritize risks using risk matrices
- Develop mitigation strategies
- Create remediation roadmap
- Define residual risk acceptance criteria
- Document compensating controls

**Risk Formula:** Risk = Threat × Vulnerability × Impact

**Output:** Prioritized risk register with actionable remediation recommendations.

#### Benefits of PASTA
- **Business-aligned:** Links technical security to business objectives
- **Comprehensive:** Covers entire threat modeling lifecycle
- **Flexible:** Adaptable to various development methodologies (Agile, DevOps, Waterfall)
- **Actionable:** Produces concrete, prioritized recommendations
- **Collaborative:** Engages stakeholders from business and technical teams

#### Implementation Best Practices
1. **Start early:** Begin threat modeling during design phase
2. **Iterate regularly:** Update threat model as application evolves
3. **Involve stakeholders:** Include developers, architects, and business owners
4. **Use automation:** Leverage tools for scanning and analysis where possible
5. **Document thoroughly:** Maintain detailed records for compliance and future reference
6. **Train teams:** Ensure development teams understand secure coding practices
7. **Integrate with SDLC:** Make threat modeling part of standard development process

---

## Additional Protection Strategies

### Defense in Depth
Implement multiple layers of security controls to protect assets if one layer fails.

### Principle of Least Privilege
Grant users and systems only the minimum access required to perform their functions.

### Security Awareness Training
Educate users about social engineering tactics, phishing indicators, and security best practices.

### Input Validation and Sanitization
Validate and sanitize all user inputs to prevent injection attacks.

### Regular Security Updates
Keep systems, applications, and security tools updated with latest patches.

### Multi-Factor Authentication (MFA)
Require multiple forms of verification to access sensitive systems and data.

### Network Segmentation
Divide networks into segments to contain breaches and limit lateral movement.

### Continuous Monitoring
Implement security information and event management (SIEM) for real-time threat detection.

### Incident Response Plan
Develop and regularly test procedures for responding to security incidents.

### Regular Security Assessments
Conduct penetration testing, vulnerability assessments, and security audits periodically.

---

## Conclusion

Protecting organizational assets requires understanding the diverse threat landscape and implementing comprehensive security measures. Social engineering exploits human vulnerabilities, malware targets technical weaknesses, and injection attacks exploit poor coding practices. By using structured methodologies like PASTA and implementing defense-in-depth strategies, organizations can significantly reduce their risk exposure and build resilient security postures.

**Remember:** Security is not a one-time effort but a continuous process of assessment, improvement, and adaptation to emerging threats.

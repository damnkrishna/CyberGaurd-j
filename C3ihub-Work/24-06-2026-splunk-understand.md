hey so as for the task of today as my exam is also going to happen on sunday i thought why not 
give it a shot i know i have less time 3 days but i can make it worth it 
but also documenting what i learned so that i can use it for my internship as well 
and for better and long lasting understanding of how splunk perform its security operation data management assest security and all those stuff


## as for the beginning i am going to start from data foundamentals

### security data management

Section 2.1: Data-driven integration
Section 2.2: Critical data sources (event, identity, asset, vulnerability)
Section 2.3: High signal/low noise analysis (EDR vs Windows process logs)
Section 2.4: Legacy/OT/IC monitoring strategies
Section 2.5: Data lifecycle (retention, tiering, residency, access)
Section 2.6: Normalization (CIM, CEF) importance
Section 2.7: Advanced analytics (ML, behavioral, AI)
Section 2.8: Scaling architectures

i will write what i understood by each one of these above mentioned section 
one line learning that i should understand and also add in my own project of building indigenenous it/ot siem tool

#### sdm(security data management)flow

Data Sources
↓
Collection
↓
Normalization
↓
Enrichment
↓
Storage
↓
Detection & Investigation

Everything becomes searchable and comparable.


#### How Security Data Management fits inside a SOC

Security Tools
↓
Collection
↓
Normalization (CIM)
↓
Enrichment
↓
Storage
↓
Correlation Searches
↓
Risk Scoring
↓
Incident Review
↓
SOAR Automation


### splunl es and cim mondel 
Raw Logs
    ↓
Field Extractions
    ↓
CIM Normalization
    ↓
Data Models
    ↓
Acceleration
    ↓
tstats Searches
    ↓
Enterprise Security Detections
    ↓
Risk-Based Alerting


A Data Model is a CIM-based, structured, logical representation of related events that provides a common and efficient way for Enterprise Security to search and analyze data without changing where the raw logs are stored.



### Important ES Data Models

You should remember these.

Data Model	Purpose
Authentication	Login activities
Endpoint	Processes, files
Network Traffic	Connections
Malware	Malware events
Web	Web activity
Email	Email events
Intrusion Detection	IDS alerts
Change	System modifications

These appear repeatedly in Enterprise Security.

tstats is a high-performance search command that queries accelerated data model summaries instead of raw events. It is commonly used by Enterprise Security correlation searches to perform detections efficiently at scale.



as the boss have also asked me to read splunk and google chromium and find what their siem have better than the siem we are building here at c3ihub
well i guess he kind of trust me and also he himself have done the research and after that he asked me to recheck or verify and put my own points 
for making it better improved version of it 

well what can i say this is great opportunity of both learning and showing that how we can improve it 





















Indexes  = Where data lives
CIM      = How data is named
Data Model = How related data is organized
Acceleration = How searches become fast
tstats = How ES queries the accelerated summaries

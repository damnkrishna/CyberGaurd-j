# Splunk Security Data Management & CIM Study Notes

## Exam Preparation Goal
- **Exam Date:** Sunday (3 days from now)
- **Objective:** Master Splunk Security Data Management, Security Operations, Asset Security, and related concepts
- **Documentation Purpose:** Create learning resources for internship and building indigenous IT/OT SIEM tool
- **Additional Goal:** Compare and improve upon existing Splunk & Google Chromium SIEM implementations for C3I Hub

---

## Part 1: Data Fundamentals - Security Data Management

### Sections to Cover

1. **Section 2.1:** Data-driven integration
2. **Section 2.2:** Critical data sources (event, identity, asset, vulnerability)
3. **Section 2.3:** High signal/low noise analysis (EDR vs Windows process logs)
4. **Section 2.4:** Legacy/OT/IC monitoring strategies
5. **Section 2.5:** Data lifecycle (retention, tiering, residency, access)
6. **Section 2.6:** Normalization (CIM, CEF) importance
7. **Section 2.7:** Advanced analytics (ML, behavioral, AI)
8. **Section 2.8:** Scaling architectures

**Approach:** Writing what I understood from each section, including one-line learnings and applications for building an indigenous IT/OT SIEM tool.

---

## Part 2: Security Data Management (SDM) Flow

### The Core SDM Flow

```
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
```

**Key Principle:** Everything becomes searchable and comparable.

---

## Part 3: How Security Data Management Fits Inside a SOC

### Complete SOC Data Pipeline

```
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
```

This pipeline ensures that security tools feed into a centralized system where data is normalized, enriched, and used for detection and response.

---

## Part 4: Splunk ES and CIM Model

### Data Processing Pipeline to Enterprise Security

```
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
```

### Understanding Data Models

**Definition:** A Data Model is a CIM-based, structured, logical representation of related events that provides a common and efficient way for Enterprise Security to search and analyze data without changing where the raw logs are stored.

---

## Part 5: Important ES Data Models Reference

| Data Model | Purpose |
|---|---|
| **Authentication** | Login activities |
| **Endpoint** | Processes, files |
| **Network Traffic** | Connections |
| **Malware** | Malware events |
| **Web** | Web activity |
| **Email** | Email events |
| **Intrusion Detection** | IDS alerts |
| **Change** | System modifications |

**Remember:** These data models appear repeatedly in Enterprise Security implementations.

---

## Part 6: tstats - The Performance Key

### What is tstats?

`tstats` is a high-performance search command that queries accelerated data model summaries instead of raw events. It is commonly used by Enterprise Security correlation searches to perform detections efficiently at scale.

**Why It Matters:** Performance and scalability at enterprise level depend heavily on tstats optimization.

---

## Part 7: Comparative Analysis Task - Splunk vs Google Chromium vs C3I Hub SIEM

### Research Objective

The boss has asked me to:
1. Research Splunk's SIEM capabilities
2. Research Google Chromium's SIEM capabilities
3. Compare them with the SIEM being built at C3I Hub
4. Identify areas where the C3I Hub SIEM can be improved
5. Provide my own analysis and recommendations

**Trust Factor:** The boss has already conducted research and is asking me to verify findings and provide my own points for creating an improved version.

**Opportunity:** This is both a learning exercise and a chance to demonstrate how improvements can be made to the existing SIEM.

---

## Part 8: The Complete SDM Hierarchy

### Full Technical Breakdown

```
2.1 Data Integration
    ↓
    Correlate multiple datasets

2.2 Critical Data Sources
    ↓
    Event + Identity + Asset + Vulnerability

2.3 High Signal / Low Noise
    ↓
    Prioritize useful telemetry

2.4 OT Monitoring
    ↓
    Passive monitoring and network visibility

2.5 Data Lifecycle
    ↓
    Retention, tiering, residency, access

2.6 Normalization
    ↓
    CIM, Data Models, DMA, tstats

2.7 Advanced Analytics
    ↓
    Behavioral analytics, ML, AI

2.8 Scaling
    ↓
    Indexer clusters, Search Head clusters, RF, SF
```

---

## Part 9: Key Splunk Architecture Concepts

### Essential Definitions

| Concept | Definition |
|---|---|
| **Indexes** | Where data lives |
| **CIM** | How data is named |
| **Data Model** | How related data is organized |
| **Acceleration** | How searches become fast |
| **tstats** | How ES queries the accelerated summaries |

These five concepts form the backbone of understanding Splunk enterprise security architecture.

---

## Part 10: Key Takeaways for Indigenous IT/OT SIEM Development

When building the C3I Hub SIEM tool, prioritize:

1. **Data normalization** similar to CIM standard
2. **Critical data source integration** (events, identity, assets, vulnerabilities)
3. **High signal-to-noise filtering** to reduce false positives
4. **Data lifecycle management** for compliance and performance
5. **Advanced analytics capabilities** for behavioral detection
6. **Scalable architecture** from day one
7. **Performance optimization** through acceleration and summary searches

---

## Study Timeline

- **Day 1 (Today):** Foundational concepts - Data Management, CIM, Data Models
- **Day 2:** Advanced topics - Scaling, OT Monitoring, Advanced Analytics
- **Day 3:** Comparative analysis and practice questions
- **Sunday Exam:** Apply all concepts

**Success Metric:** Not just passing the exam, but building practical knowledge applicable to the internship and C3I Hub project.

# OT / ICS Security — Notes

So I got to know that IT and OT are two different things. Here's what I want to lay out — the steps, the architecture these OT systems use. Consider the example of a pizza company to get it.

OT checks the physical info and verifies if the values are working properly.

---

## 1. OT and ICS

### Architecture Levels

Data from sensors is read by PLCs. They sense the value directly from the hardware, and if it passes a certain threshold, it stops itself — stopping it from causing a major accident.

As for the DCS, it's a complex single-function checker. It checks a specific function and verifies if it's working properly or not. Based on all that, if things are normal or just above normal, it's fine — otherwise, there's a threshold value set to stop a major incident from happening.

All these values are observed centrally by SCADA, which acts as a watchtower, observing everything and deciding if there's any need to take action on any certain stuff.

---

### The Purdue Model (Level Breakdown)

| Level | Name | Description |
|---|---|---|
| **Level 0** | The Physical Process | The actual sensors, valves, motors, and oven burners. (The physical hardware.) |
| **Level 1** | Basic Control (PLCs) | The tough microcomputers physically wired to Level 0. They read the sensors and open/close valves to keep things safe. |
| **Level 2** | Supervisory Control (DCS / HMI) | The local control screens on the factory floor. Allows humans to adjust the speed of a specific assembly line or change a localized setting. |
| **Level 3** | Site Operations (SCADA) | The central watchtower. Collects data from all the PLCs and DCS systems across the whole factory (or multiple factories) to give the big picture. |
| **Level 3.5** | The Industrial DMZ | A heavily guarded digital checkpoint. Sits between the OT network (the kitchen) and the IT network (the front office) to make sure no internet hackers can easily jump down into the kitchen. |
| **Level 4 & 5** | Enterprise IT | The front office — corporate emails, customer databases, and internet access. |

---

## 2. Protocols

### Raw Network Telemetry

#### Modbus TCP
- Oldest and simplest.
- Operates on a client/server model.
- Strict teacher (asking roll call) — 24×7.
- Waits for a turn before sending another message.

**Lacks:**
- Encryption
- Authentication
- Transmits clear text data → insecure

---

#### DNP3 (Distributed Network Protocol)
- Event-driven (raise your hand if queried) → otherwise stay silent.
- Categorizes data into classes (Class 0 to 3).
- Only sends a message when a specific event happens.

---

#### IEC 61850 — Works over digital network connections (rather than direct wiring)

**MMS (Manufacturing Message Specification)**
- Used for routine, detailed paperwork.
- Just like an email or a formal report.

**GOOSE (Generic Object-Oriented Substation Event)**
- For extreme emergencies (like a power line snapping).
- Skips all the normal internet rules.
- Blasts a super fast, repeating signal directly to the system to cut the power before a disaster happens.

---

### Protocol Summary

| Protocol | Analogy | Behavior |
|---|---|---|
| Modbus | Strict Teacher Roll Call | Continuous back-and-forth polling |
| DNP3 | Raising Your Hand | Only sends data when an event happens |
| MMS (IEC 61850) | The Report Card | Normal, detailed data reporting |
| GOOSE (IEC 61850) | The Fire Alarm | Instant emergency signals that skip the rules |

---

## 3. C3iHub — Specific Defense Projects / Tools

### a. CSCMM — The Health Checkup Scorecard
- A grading system to see how well you use your tools.
- Specifically tailored for India's critical sector to measure how prepared they are for cyber war.
- Ranges from Level 1 (doors are unlocked) to Level 5 (armed guards and lasers).

---

### b. CPS Intrusion Detection — RobustD (The Physics Cop)
- Understands the physical behavior of machines, not just the digital code or logs.
- Checks for commands that don't make sense in the real world.

---

### c. ICS Kill Chain — Playbook for Destruction
- Focuses entirely on the steps an attacker takes to cause physical destruction, rather than just data theft.
- The ICS Kill Chain ends with an explosion, blackout, or water contamination.

---

### d. Indigenous IT/OT Security Operations Center
A 100% homegrown SIEM and SOC platform that monitors both the digital network (IT) and the physical machinery network (OT).

Deployed at:
- Bhilai Steel Plants (SAIL)
- National Highways Authority of India (NHAI) → C3iVazara
- Indian Ports Association (IPA)

---

### e. BlockStash — Cyber Forensics and Cybercrime Tracking
- Tracks illicit activities in crypto transactions.
- Helps in tracing money dealing in Bitcoin or any other cryptocurrency.
- Keeps track of these transactions without needing to share private information with foreign tools or private agencies.

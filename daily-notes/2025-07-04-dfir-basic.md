# DFIR: An Introduction

As we never know when any security breach happens, we can fix vulnerabilities but can't stop the thinking and unique ways used by hackers to use vulnerabilities in web applications. Hence, it is very important to set up some clean set of rules to perform when any security breach happens - that is called DFIR: Digital Forensics and Incident Response.

As we know, when a security breach happens, they just don't run the hack at the same time. This is both for avoiding suspicion but also to set up themselves to find out important tasks. But here DFIR comes into play - as soon as we get slight info that some data breach has happened, we can start finding digital traces left by the hacker to get back to him and find the info already gone and stop it from hacking more.

## Key Objectives of DFIR

- Finding evidence of attacker activity in the network and sifting false alarms from actual incidents
- Robustly removing the attacker, so their foothold from the network no longer remains
- Identifying the extent and timeframe of a breach. This helps in communicating with relevant stakeholders
- Finding the loopholes that led to the breach. What needs to be changed to avoid the breach in the future?
- Understanding attacker behavior to pre-emptively block further intrusion attempts by the attacker
- Sharing information about the attacker with the community

## Required Expertise

As people who are in this DFIR field have to have expertise in two areas:
- Digital forensics
- Incident response

## Core DFIR Concepts

### Artifacts
Pieces of evidence that point to an activity that has been performed on a system.

### Evidence Preservation
We have to preserve the evidence so sometimes while finding more info from the evidence, we hamper or break the evidence. So it is very important to maintain a write-up or similar evidence in safety which can be used if the first got affected or broken during checking.

### Chain of Custody
Evidence should be in some safe hands so evidence won't be replaced or contaminated while shifting - very important in serious cases.

### Order of Volatility
It refers to a person who is collecting evidence should have info about the evidence's way of storing data. For example, if evidence is in hard drive it is safe and will not be deleted even if we shutdown the device, but whereas if the data is stored in RAM it will be removed if system shuts down. Hence it is important to know about the evidence as it can delete the whole evidence forever.

### Timeline Creation
It is nothing but joining points and creating a story with timeline to prove the evidence.

## DFIR Tools

There are several tools that help in DFIR process for better and quick forensics using tools that are worldwide accepted and used by professionals:

- Eric Zimmerman's tools
- Kape
- Autopsy
- Volatility
- Redline
- Velociraptor

## DFIR Process Steps

Steps taken by professionals for DFIR:

### Preparation
Before an incident happens, preparation needs to be done so that everyone is ready in case of an incident. Preparation includes having the required people, processes, and technology to prevent and respond to incidents.

### Identification
An incident is identified through some indicators in the identification phase. These indicators are then analyzed for false positives, documented, and communicated to the relevant stakeholders.

### Containment
In this phase, the incident is contained, and efforts are made to limit its effects. There can be short-term and long-term fixes for containing the threat based on forensic analysis of the incident that will be a part of this phase.

### Eradication
Next, the threat is eradicated from the network. It has to be ensured that a proper forensic analysis is performed and the threat is effectively contained before eradication. For example, if the entry point of the threat actor into the network is not plugged, the threat will not be effectively eradicated, and the actor can gain a foothold again.

### Recovery
Once the threat is removed from the network, the services that had been disrupted are brought back as they were before the incident happened.

### Lessons Learned
Finally, a review of the incident is performed, the incident is documented, and steps are taken based on the findings from the incident to make sure that the team is better prepared for the next time an incident occurs.

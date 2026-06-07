# Day Log — Indigenous SIEM Build Sprint

## What Went Down

My whole day yesterday went in mapping all the stuff we need for setting up our own indigenous SIEM.

Earlier we were using Wazuh to normalize our logs — but not anymore. Now we are building our own, writing our own backend and frontend, normalizing our own raw logs from **Windows Security + Sysmon**, and mapping it with **OCSF format**.

We are using an open source language for that normalization and doing the mapping ourselves manually.

So half the day I read every single Event ID, mapped it with OCSF format, read and figured out which would be the best fit for it. Created an Excel sheet, analyzed **20 techniques**, and found that around **40 can be directly mapped** — but around **70 are still to be mapped** because of lack of proper findings, so those have to be done manually.

---

## The 2-Day Hackathon Ahead

As the conference is in **2 days**, we have to:

- Build, map, and normalize the whole setup — **removing Wazuh completely**, using our own normalization pipeline
- Write **~100 custom detection rules** around those mapped techniques
- Deploy everything on the SIEM
- Test it end-to-end — check if alerts are firing or just getting stored, and validate the whole pipeline

Work is going crazy. Basically a **2-day hackathon**.

---

## Team & Vibe

Team is great. Work is perfect. High pressure, high result.

---

## Extra Stuff

> *(Things I might want to revisit or think about later — added separately, not part of the original log)*

### On the OCSF Mapping

- The ~70 techniques that can't be directly mapped are going to need a decision: do we flag them as "best-effort mapped" or leave them as unmapped until proper event evidence exists? Worth deciding before writing rules around them.
- The open-source normalization language being used here — probably worth documenting which one and any quirks that show up during implementation. Good to have this locked down before the sprint ends.
- Field-level mismatches between Windows Security and Sysmon (e.g., same concept, different field names) might cause rule logic to diverge — consider a shared field alias layer in the pipeline if the normalization tool supports it.

### On the Detection Rules

- ~100 rules in 2 days is aggressive. Prioritize by technique coverage and highest-fidelity signal — the 40 directly-mapped ones should be baseline-stable, the manual 70 are where false positive risk is higher.
- Stateless vs. stateful detection split is going to matter here. Rules that need cross-event correlation (e.g., recon chains, staged execution) will need a state backend or alert store even with your own pipeline — same constraint as before, just now fully in-house.
- If there's no time to build the correlator before the conference, consider tagging rules by correlation-dependency so it's clear post-demo what's "complete" vs. "needs correlation layer."

### On Going Full In-House (Removing Wazuh)

- Biggest risk area: normalization coverage gaps. Wazuh's agent handled a lot of edge cases silently. First few days post-cutover will probably surface events that weren't in the mapping exercise.
- Logging the pipeline's ingestion failures explicitly will save debugging time — even a simple drop counter per Event ID is useful.
- If the frontend is also being written fresh, minimum viable view for the conference is probably: alert list, rule name, MITRE technique tag, raw event. Everything else can come later.

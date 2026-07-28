# C3iHub — Internship Wrapped (May 27 – July 27, 2026)

Two months done. Writing this down mostly so I remember what actually happened here, not the polished version.

## The setup

Seated in VAPT but my real work was detection engineering on Anvesha, C3iHub's in-house IT/OT SOC platform. First couple days were just getting my head around why this platform needs to exist at all — IT security assumes confidentiality-first, TCP/IP-type protocols. OT is the opposite: availability and safety first, running on Modbus, DNP3, IEC 60870-5-104, IEC 61850, OPC-UA — stuff that was never built with auth or encryption baked in. Once that clicked, the rest of the internship made a lot more sense.

## What I walked into

Got full platform access in week 2 and immediately hit ~84,000 undocumented Suricata signatures and ~40,000 Wazuh rules. No documentation, no structure. Had to consciously not try to boil the ocean and just scoped down to Reconnaissance first. That decision — narrow scope deliberately instead of panicking about the size of the thing — ended up being the pattern for the whole internship.

## The actual work, roughly in order

- Started with Sigma rules against MITRE Recon techniques, HIDS+NIDS correlation exploration.
- Week 3 was rough — correlation rules were noisy as hell. Dug into why, rewrote them, got a single test host from 180+115 alerts/day down to 4 high-fidelity alerts. That felt like the first real "I did something" moment.
- Also found the MFA-fatigue gap around then — checked whether push-notification MFA fatigue (T1621) was even detectable from Sysmon/Windows Security logs. It's not. That kind of thing happens at the Identity Provider layer, need Azure AD/Okta/Duo logs. Documented it honestly instead of shipping a rule that wouldn't fire. Small thing but it mattered to me — easy to fake coverage, harder to say "we can't see this yet."
- Bharat Innovate showcase in Nice, France happened week 4, my rules were part of what got shown. Watched it remotely while still writing new rules and starting Splunk cert prep. Weird feeling, work you wrote showing up on stage somewhere you've never been.
- Around this point I switched to manual rule-writing entirely. Noticed AI-assisted generation kept defaulting to whatever single log source had the least noise, instead of actually building something resilient across sources. That was the real turning point of the internship for me — decided I didn't trust the automated stuff for anything security-critical after that.
- Started grounding everything against SigmaHQ, LOLBAS, Atomic Red Team, SwiftOnSecurity Sysmon config instead of writing from scratch every time. Made the work faster and more consistent.
- Splunk cert prep (Cybersecurity Defense Architect) ran in parallel — exam got rescheduled because of a platform-side issue on their end, not mine, which was mildly annoying but not something I could control.
- Weeks 6-8 were mostly grind: daily write-backtest-approve-promote cycle, 20-25 rules a day, consolidating inventory, chasing the technique coverage number up. Also built out the whole red-team readiness picture — what log sources and Event IDs need to be on, known gaps (no Linux agent, no SSL-inspection proxy yet, renamed-binary evasion still possible), so someone could test this without me being in the room.
- Last week was just closing everything out — full doc pass, synced to GitHub, handoff notes for EDR and SIEM/correlation both.

## Numbers, for the record

- 696 rules total — 546 Sigma + 150 JSON correlation, across 472 files
- ~195 of 222 MITRE ATT&CK parent techniques mapped
- 453 rules marked production-ready as of the last dashboard snapshot
- Noise reduction: 295/day → 4/day on the test host

## What I'm actually taking away from this

Detection engineering is a scoping and judgment problem way more than it's a rule-writing problem. Anyone can write a Sigma rule. Deciding what's worth detecting, what log source actually gives you signal vs noise, and being honest about what you *can't* see yet — that's the actual skill, and I don't think I understood that going in.

Also learned I don't fully trust automation for this kind of work yet, at least not unsupervised. That's probably going to shape how I approach tooling in whatever I do next.

Karthik sir's push toward manual rigor over shortcuts is probably the single biggest influence on how I think about this now. Divyanshu bhaiya kept the day-to-day sane. Good two months, not always easy, but I came out of it actually thinking differently about the work — not just with a longer resume line.

Repo, if I ever want to look back at the actual rules: github.com/damnkrishna/Detection-Engineering-Ruleset

Back to job hunting now.

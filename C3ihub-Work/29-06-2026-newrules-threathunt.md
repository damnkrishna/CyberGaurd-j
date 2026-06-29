# What I Learned Today: Threat Hunting, Backtesting, and My Rule Writing Plan

So today sir told me he is currently working on adding **threat hunting** into the tool we are building. Naturally I had no idea what that exactly meant, so he explained it to me.

He said — whenever we push a new rule, before the final push, it will scan through the stored logs and tell us: *"Based on this rule, here is what information can be found, and these are the alerts that would have been generated if this rule was already active."*

Basically, it helps us decide whether a rule is even worth writing or pushing in the first place. And honestly? The idea is really good.

---

## Wait — That's Not Actually Threat Hunting

After thinking about it more and reading up on it, I realized there is a slight mix-up in the terminology here. What sir described is actually called **Rule Backtesting** (also known as Historical Replay or Retrospective Scanning). Google Chronicle calls this exact feature **"Retrohunt"**.

It is a tool *used by* threat hunters — but it is not threat hunting itself. Let me break down what each one actually is.

---

## What Sir Is Actually Building: Rule Backtesting

When you are building a stream-based SIEM, a bad rule is genuinely dangerous. If you push a poorly written Sigma rule directly onto the live stream, it could trigger thousands of false positives in minutes and just completely overwhelm the SOC analysts.

The feature sir is designing prevents exactly that. It works like this:

1. You write a new detection rule (draft stage)
2. The engine runs that rule against the last 30 days of stored historical logs
3. It tells you — *"If this rule had been active last month, it would have fired 450 times"*
4. If 450 is too noisy, you go back and refine the rule before pushing it to the live real-time stream

This is a **Detection Engineering** feature. It is basically a quality control layer for your automated alerts. Really solid thing to have in a SIEM.

---

## So What Is Actual Threat Hunting?

**Threat Hunting is a proactive, human-driven process where you actively search through networks to detect and isolate advanced threats that evade existing security solutions.**

The key difference is this — if a SIEM's automated rules catch an attack, that is *Detection*. Threat Hunting starts with a completely different assumption:

> *"The rules failed. We are already breached. Let's go find them."*

A real threat hunt looks something like this:

**Step 1 — Form a Hypothesis**
The analyst does not wait for any alert. They create a theory on their own. For example: *"I think attackers might be bypassing our endpoint detection by using legitimate Windows admin tools — Living off the Land."*

**Step 2 — Deep Dive Queries**
They manually write complex, ad-hoc queries against stored data to look for very specific, unusual behaviors that no automated rule is currently watching for.

**Step 3 — Investigate Anomalies**
They find something strange — like a regular marketing employee running PowerShell scripts at 3 AM.

**Step 4 — Operationalize**
Once the hunter confirms it is a new attack technique, *then* they write a new rule to automate detection of it going forward.

So detection is passive (the system alerts you). Threat Hunting is active (you go looking for the threat yourself).

---

## How Both Connect in Our Platform

Sir is actually steering the architecture in exactly the right direction — because backtesting is what bridges the gap between hunting and detection.

When a threat hunter finds a new zero-day behavior manually, they need to turn it into an automated rule. Before dropping that freshly written rule onto our ultra-fast stream processor, they use the backtesting feature to make sure it is perfectly tuned against historical data first.

Backtesting ensures that when a hunt becomes a detection, it does not break the system.

---

## My Plan: 20–25 Rules Daily

Okay so beyond all this terminology stuff, I have also figured out a process I want to follow for writing and pushing rules — something that makes sense both technically and practically.

Here is what I am thinking:

**Step 1 — Write 20–25 rules daily**
Instead of trying to push a hundred rules at once and testing them all at the end, I will write a smaller focused batch every day.

**Step 2 — Verify on platform first**
Before anything gets pushed, I will run them through the platform to check the real effect — basically use the backtesting feature to see what kind of output each rule produces.

**Step 3 — Ask mentor before pushing**
Once I am satisfied with how a rule looks, I will take permission from my mentor to push it in **logging mode only** — not directly to alerting. This way we can observe the behaviour without causing noise for the actual team.

**Step 4 — Monitor for a day**
Let it run in logging mode for about a day. If it is working properly and not generating garbage, then we push it to the active stream.

---

## Why This Process Makes Sense

The biggest mistake in detection engineering is writing a ton of rules and testing them all at the last minute. That is a disaster waiting to happen.

By doing this daily — writing, verifying, getting approval, logging, then pushing — I am spreading the testing load across the entire timeline. By the time final review comes, most of the work is already done and already validated. No last-minute panic, no bulk noise flooding the SOC.

It also keeps my mentor in the loop without bothering them every five minutes. One clean batch per day, already pre-verified on my end, ready for a quick approval.

Honestly I think this workflow is going to save a lot of headaches down the line.

---

*This is just me documenting my thought process as I learn — things might change as I get deeper into the platform. But for now, this is the plan.*

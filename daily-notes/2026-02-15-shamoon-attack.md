# Shamoon Attack

It was a logic bomb created by a hacker group named **Cutting Sword of Justice** — they took complete responsibility of the attack.

Their main target was national oil companies that are indirectly or directly helping USA:

- **Saudi Aramco** (Saudi Arabia)
- **RasGas** (Qatar)

---

## Effect

- 30,000 computers destroyed — complete data deletion, even OS and hardware damage
- Supply of oil stopped, complete shutdown
- Shutting around 25% of world oil distributions
- Burning US flag left on computer screen = political agenda (work of a nation state)

---

## Time of Attack

**Wednesday, 15th August 2012 at 11:08 AM** (local time, Saudi Arabia)

---

## Design of the Attack

The malware was designed to erase and overwrite hard drive data with a corrupted image and report back the address of infected computers.

**The Malware → Logic Bomb**
- Triggered master boot record and data wiping payload

**Dropper: NtsSrv**
- 32-bit and 64-bit versions
- Checks if 64-bit is present → returns 64-bit, otherwise 32-bit

**Wiper: RawDisk**
- Achieves direct user-mode access to a hard drive without using Windows API

**Reporter**
- Returns details about updated/hacked/breached computers back to the network

---

## In-Depth: Attack Chain

This research led analysts to believe that the actor using Shamoon relied heavily on weaponized documents built to leverage PowerShell to establish their initial network foothold:

1. Attackers send a **spear phishing email** to employees at the target organization — the email contains a Microsoft Office document as an attachment
2. Opening the attachment invokes **PowerShell** and enables command line access to the compromised machine
3. Attackers can now communicate with the compromised machine and remotely execute commands on it
4. Attackers use their access to deploy additional tools and malware to other endpoints or escalate privileges
5. Attackers study the network by connecting to additional systems and locating critical servers
6. The attackers deploy the **Shamoon malware**
7. A coordinated Shamoon outbreak begins and computer hard drives across the organization are **permanently wiped**

---

## My Take — The Real Story Behind Shamoon

As far as I know, the **Stuxnet attack** done by US and Israel on Iran's nuclear facility was the reason behind this attack. Iran wanted to publicly humiliate, damage and punish the US for what they did.

They didn't want stealth like Stuxnet — they wanted to show it. They wanted to let them know who the target is. That's why at the end they left a burning US flag on affected computers.

And I think they deliberately chose **not to directly target the US** — that would've been less painful, and maybe it was tougher for them too. The US was likely aware of the consequences of Stuxnet and the risk of getting hit back.

But intelligent Iran took the right decision — hurt **two targets at once**:
- Their soul rival, Saudi Arabia
- The oil resources that were the energy pillar for the US

Their actual target wasn't just oil production — it was **US influence + Gulf economic stability**.

---

## Shamoon vs Stuxnet — Compared

| | Stuxnet | Shamoon |
|---|---|---|
| Goal | Targeted sabotage (centrifuges only) | Destroy entire IT environment |
| Stealth | Maximum — tried to hide | None — wanted to be seen |
| Exploit sophistication | Elite zero-day chain | Zero zero-days, no sophistication |
| Approach | Surgical precision | Access and damage |
| Message | Silent disruption | Public political statement |

Compared to Stuxnet, Shamoon was **not well documented**. Nothing was tested publicly, no information about any testing exists. It was not an elite exploit chain attack — it relied on **access and damage**, not brilliance.

> **Stuxnet tried to hide. Shamoon wanted to be seen.**

Shamoon used zero zero-day attacks — nothing complicated, nothing sophisticated. Just a clean, simple bomb with a huge impact. No stealth.

---

## Shamoon Mapped to MITRE ATT&CK

> **Key framing**: Shamoon is a textbook case of *low-exploit, high-impact* tradecraft. Almost every technique abuses **legitimate enterprise features**, not software bugs.

---

### 1. Initial Access — T1078: Valid Accounts

**Most important technique.**

Attackers used legitimate credentials, likely stolen from compromised users, IT admins, or contractors. No exploit needed — this bypasses most perimeter defenses and makes activity look completely normal.

> *"Initial access was achieved via the use of valid domain credentials, eliminating the need for exploit-based entry."*

---

### 2. Execution

**T1059 — Command and Scripting Interpreter**
Shamoon executed commands using native Windows utilities, batch execution, and possibly PowerShell in later variants. Living-off-the-land. Reduces malware footprint. Harder to detect via signatures.

**T1053 — Scheduled Task / Job** *(Logic bomb delivery)*
Malware scheduled execution at a specific time, ensuring synchronized destruction with no external command needed. This turned Shamoon into an **autonomous weapon** — even if defenders detected it early, the payload still detonated.

---

### 3. Persistence — T1547: Boot or Logon Autostart Execution

Shamoon ensured execution after reboot, critical for wiping MBR and preventing recovery. Persistence here wasn't for longevity — it was for **guaranteed detonation**.

---

### 4. Privilege Escalation — Operational Admin Abuse

Important nuance: Shamoon did **not** exploit a kernel bug. It relied on already-elevated accounts.

> *"Privilege escalation was operational rather than exploit-driven."*

---

### 5. Lateral Movement

**T1021 — Remote Services**
Used internal Windows services — SMB, admin shares, remote execution. No worm behavior, no scanning noise. Quiet but fast internal spread.

**T1080 — Lateral Tool Transfer**
Malware copied itself across network shares and internal file servers. Trusted infrastructure, abused.

---

### 6. Defense Evasion

**T1070 — Indicator Removal on Host**
File overwriting eliminated logs, artifacts, and forensic evidence. This wasn't stealth — it was **post-destruction denial**.

**T1036 — Masquerading**
Shamoon components appeared as legitimate files and normal system activity. This delayed detection long enough for detonation.

---

### 7. Command and Control — T1071: Application Layer Protocol

The reporter module attempted outbound communication, often failing or becoming irrelevant.

> Shamoon was **not C2-dependent** — making it resilient against network isolation, sinkholing, and C2 takedowns.

---

### 8. Impact

**T1485 — Data Destruction** *(Primary goal)*
Overwrote files with junk data. No encryption. No recovery path.

**T1490 — Inhibit System Recovery**
Corrupted the Master Boot Record and system files. Machines became unbootable.

**T1499 — Endpoint Denial of Service**
~30,000 systems rendered unusable. Business operations severely disrupted.

---

### 9. Psychological & Strategic Impact

**T1491 — Defacement**
The burning US flag image left behind was **intentional signaling** — attribution, political messaging, morale and reputational damage. Not noise.

---

### Full Technique Summary

| ATT&CK Tactic        | Technique                         |
|----------------------|-----------------------------------|
| Initial Access       | T1078 – Valid Accounts            |
| Execution            | T1059 – Command Interpreter       |
| Execution            | T1053 – Scheduled Task            |
| Persistence          | T1547 – Autostart Execution       |
| Privilege Escalation | Operational admin abuse           |
| Lateral Movement     | T1021 – Remote Services           |
| Lateral Movement     | T1080 – Tool Transfer             |
| Defense Evasion      | T1070 – Indicator Removal         |
| Defense Evasion      | T1036 – Masquerading              |
| C2                   | T1071 – Application Protocol      |
| Impact               | T1485 – Data Destruction          |
| Impact               | T1490 – Inhibit Recovery          |
| Impact               | T1499 – Endpoint DoS              |
| Impact               | T1491 – Defacement                |

> **Shamoon demonstrates that destructive cyber operations do not require advanced exploits — only sufficient access, timing, and intent.**

---

## Final Summary — Three Hard Truths

Shamoon showed three hard truths:

1. **Cyberwar has real economic impact**
2. **Attribution is murky → retaliation risk increases**
3. **Once cyber weapons are used, they never go back in the box**

That's why today's attacks on power grids, oil, hospitals, and satellites all trace their lineage back to Stuxnet → Shamoon.

---

### The Chain Reaction of Cyber Warfare

```
Stuxnet (US/Israel → Iran)
        ↓
Iran adopts disruptive cyber retaliation (Shamoon, DDoS)
        ↓
Cyber becomes normalized as statecraft (China: OPM hack)
        ↓
Cyber becomes mass-destructive and indiscriminate (Russia: NotPetya)
```

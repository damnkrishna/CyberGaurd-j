
# Sysmon — Practical Summary (What it is, how to use it, and what actually matters)

## 1. What Sysmon *actually* does
Sysmon (from **Sysinternals / Microsoft**) is a **low-level system activity logger** for Windows.

It does NOT:
- Block attacks  
- Act as an antivirus  
- Correlate events automatically  

It DOES:
- Log detailed system activity into **Windows Event Logs**
- Help you **reconstruct attacks after or during an incident**

Think of it as:
> A high-resolution CCTV camera for your system, not a security guard.

---

## 2. What kind of data Sysmon gives you
Key high-value events:

| Event ID | What it logs | Why it matters |
|----------|-------------|----------------|
| 1 | Process Creation | Detect malware execution, command-line abuse |
| 2 | File Creation Time Change | Detect timestomping |
| 3 | Network Connections | Detect C2 communication |
| 7 | Image/DLL Load | Detect DLL injection |
| 8 | CreateRemoteThread | Process injection |
| 10 | Process Access | Credential dumping |
| 11 | File Create | Dropped malware |
| 13 | Registry Value Set | Persistence |
| 22 | DNS Query | Beaconing / exfiltration |

---

## 3. Core idea behind this config (SwiftOnSecurity config)

This config is:
- **High-signal focused**
- **Noise-reduced**
- Designed for **manual investigation**

Key philosophy:
> Instead of logging everything → log what matters and filter known-noise at source.

---

## 4. Most important concept: INCLUDE vs EXCLUDE

### Rule logic:
- `onmatch="include"` → log ONLY what matches
- `onmatch="exclude"` → log EVERYTHING except what matches

### In this config:
- **ProcessCreate uses EXCLUDE**
  → Logs almost everything, except known safe noise

- **NetworkConnect uses INCLUDE**
  → Logs only suspicious behavior

---

## 5. What to focus on (real-world usage)

### 1. Process Creation (Event ID 1)
This is your **#1 signal**

Look for:
- Suspicious parent-child relationships  
  - `winword.exe → powershell.exe`
- Weird command lines  
- Execution from:
  - `C:\Users`
  - `C:\Temp`
  - `C:\ProgramData`

---

### 2. Network Connections (Event ID 3)
This config logs only suspicious sources.

Focus on:
- `powershell.exe` making outbound connections
- `cmd.exe`, `mshta.exe`, `certutil.exe`
- Anything from:
  - Temp folders
  - User directories

---

### 3. Persistence (Registry + File events)
Watch for:
- Autoruns
- Scheduled tasks
- Registry modifications

---

### 4. File Timestomping (Event ID 2)
Red flag:
- Executables with modified timestamps
- Activity in shadow copies

---

## 6. Key detection philosophy

### Don't trust:
- Process names
- File paths alone

Because attackers:
- Rename malware (`chrome.exe`, `svchost.exe`)
- Drop files in legit directories

---

### Always correlate:
- Process + Parent
- CommandLine
- File path
- User context

---

## 7. Important things to keep in mind

### 1. Sysmon is NOT tamper-proof
- Admin-level attacker can disable it

---

### 2. Noise is the biggest problem
Especially:
- DNS logs (Event ID 22)

Tip:
- Disable DNS if you're beginner
- Or filter heavily

---

### 3. Legit tools can be malicious
Examples:
- `powershell.exe`
- `certutil.exe`
- `mshta.exe`

These are called:
> Living-off-the-land binaries (LOLBins)

---

### 4. Filtering is critical
Bad filtering = blind system  
Over-filtering = missed attacks  

Balance is everything.

---

## 8. How to configure Sysmon (practical steps)

### Step 1: Install Sysmon
```bash
sysmon.exe -i sysmonconfig.xml
````

### Step 2: Update config

```bash
sysmon.exe -c sysmonconfig.xml
```

### Step 3: Remove Sysmon

```bash
sysmon.exe -u
```

---

## 9. Where to view logs

Open:

```
Event Viewer → Applications and Services Logs → Microsoft → Windows → Sysmon → Operational
```

---

## 10. How to get good at Sysmon (this is what actually works)

### Phase 1 (You are here)

* Understand event IDs
* Read logs manually

---

### Phase 2

* Simulate attacks:

  * Run `powershell download cradle`
  * Use `nmap`, `netcat`
* Observe logs

---

### Phase 3

* Build detection rules
* Map to MITRE ATT&CK

---

### Phase 4

* Integrate with:

  * SIEM (Splunk, ELK)
  * WEF (Windows Event Forwarding)

---

## 12. What you should focus on (no distractions)

If you're serious about cybersecurity:

1. Master:

   * Process trees
   * Command-line analysis

2. Practice:

   * Detecting abnormal execution paths

3. Ignore:

   * Memorizing config lines blindly

---

## 13. Brutal truth

Just reading Sysmon config = useless

What makes you dangerous:

* Replaying attacks
* Seeing logs
* Connecting behavior → detection

---

## 14. Simple mental model

```
User action → Process → Child Process → Network → Persistence
```

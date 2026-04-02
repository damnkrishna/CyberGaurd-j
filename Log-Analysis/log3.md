# SOC Analysis Report — Suspicious Outbound Connection via PowerShell

**Analyst Role:** SOC Analyst

**Log Source:** Sysmon

**Investigation Trigger:** Unexpected outbound network connection from a user process

You suspect that a process on your system is making unexpected outbound connections. Your task is to identify, investigate, and explain the behavior using Sysmon logs.
---

## Command Executed

```powershell
powershell -nop -w hidden -c "Invoke-WebRequest http://example.com"
```

---

## Initial Observation

As soon as the command was entered, the terminal hid itself. This is because of the `-w hidden` flag — it ran the process in the background to hide what was happening from the user.

---

## Processes Identified

After the command executed, Sysmon captured the creation of the following processes:

- `msedge.exe`
- `powershell.exe`
- `conhost.exe`
- `WindowsTerminal.exe`

I'm not sure whether all of these are part of the malicious activity or just background/distraction processes. The one that clearly matters here is `powershell.exe` — it is the one doing the actual work.

---

## Network Activity

Sysmon captured an outbound connection made by `powershell.exe`:

| Field | Details |
|---|---|
| Process | `powershell.exe` |
| Destination | External IPv6 address |
| Destination Port | 80 |
| Source Port | 59690 |
| Protocol | TCP |
| Connection Type | HTTP |
| Resolution | DNS via TCP |

---

## Files Downloaded

The following `.ps1` files were created on disk:

- `policytest.kem.ps1`
- `policytest.4bu.ps1`

The parent process ID of these file creation events traces back to `powershell.exe`, which confirms that PowerShell was the one downloading these files from the external source.

---

## Conclusion

`powershell.exe` made an outbound HTTP connection to an external IPv6 address on port 80, downloaded two PowerShell script files, and did all of this while keeping the terminal hidden from the user.

The file creation events in Sysmon confirmed the parent process was `powershell.exe`, which ties the network activity and the file drops together.

<img width="800" height="900" alt="image" src="https://github.com/user-attachments/assets/a1d293c0-b056-48e9-a86f-7973c46da92d" />

# 📝 SOC ANALYSIS REPORT 

## 🔹 Alert Summary

A suspicious PowerShell execution was observed generating network traffic and creating script files on the system.

---

## 🔹 Data Source

* **Sysmon Logs**

  * Event ID 1 (Process Creation)
  * Event ID 3 (Network Connection)
  * Event ID 11 (File Creation)

---

## 🔹 Observations

### 1. Process Execution (Event ID 1)

* **Process:** `powershell.exe`
* **Command Line:**

  * Included flags such as `-nop` and `-w hidden`
* **Behavior:**

  * PowerShell executed in hidden mode
  * No profile loaded

👉 **Analysis:**
This execution pattern is commonly associated with obfuscated or stealthy script execution.

---

### 2. Network Activity (Event ID 3)

* **Process:** `powershell.exe`
* **Protocol:** TCP
* **Destination Port:** 80 (HTTP)
* **Connection Type:** Outbound

👉 **Analysis:**
PowerShell initiating outbound HTTP communication is **uncommon for normal user activity** and may indicate script-based data retrieval.

---

### 3. File Creation (Event ID 11)

* **Files Created:**

  * `PolicyTest.kem.ps1`
  * `PolicyTest.4bu.ps1`
* **Parent Process:** `powershell.exe`

👉 **Analysis:**
PowerShell created temporary `.ps1` script files during execution. These may represent:

* Temporary execution artifacts
* Script staging behavior

Further inspection of file contents is required to confirm intent.

---

### 4. Process Relationships

Observed related processes:

* `powershell.exe`
* `conhost.exe`
* `WindowsTerminal.exe`
* `msedge.exe`

👉 **Analysis:**
These processes are consistent with normal Windows execution flow and do not independently indicate malicious activity.

---

## 🔹 Timeline of Events

1. PowerShell process initiated (hidden execution)
2. Outbound network connection established
3. Script files created on disk

👉 Indicates a **process → network → file creation chain**

---

## 🔹 Risk Assessment

| Indicator                   | Severity  |
| --------------------------- | --------- |
| Hidden PowerShell execution | ⚠️ Medium |
| Outbound HTTP connection    | ⚠️ Medium |
| Script file creation        | ⚠️ Medium |
| Known benign domain         | ✅ Low     |

👉 **Overall Classification:**
**Suspicious but likely benign (lab-generated activity)**

---

## 🔹 Conclusion

The observed activity demonstrates behavior commonly associated with malicious scripts, including hidden PowerShell execution and outbound network communication. However, due to the use of a known benign domain and lack of persistence or privilege escalation, the activity is assessed as **non-malicious in this context**.

---

## 🔹 Recommended Actions

* Verify contents of created `.ps1` files
* Monitor for repeated or similar behavior
* No immediate containment required

---

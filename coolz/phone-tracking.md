#  Phone Number Tracking & Device Tracing

### 1. Who Has Access

* Only **two authorities** can directly use IMSI/IMEI to trace devices:(they have permission)

  * **Telecom Provider Companies**
  * **Law Enforcement**

### 2. IMEI & IMSI

* **IMEI (device identifier)** → identifies the hardware.
* **IMSI (subscriber identity)** → identifies the SIM.
* Users can find their own IMEI/IMSI, but **can’t use it for tracking**.

  * Police/carrier can use them to block or trace the device.

### 3. Backbone Protocols

* **SS7 (Signaling System No. 7)** → telecom backbone protocol.

  * Built in an era of trust.
  * Initially only national carriers had access → now some 3rd parties also do.
* **SIGTRAN** → SS7 over IP networks.

**What can be done using SS7?**

* Location tracking
* Call & SMS interception
* Eavesdropping
* IP & data session info

### 4. How Phone Number Tracking Works

* Every SIM card has:

  * **IMSI (subscriber identity)**
  * **IMEI (device identity)**
* Phone connects to a **cell tower** → location is logged.
* **Triangulation** from multiple towers → approximate position.
* **GPS chips** → precise location.

**Surveillance Tech:**

* **IMSI catchers / fake cell towers** (e.g., StingRays, Pegasus).
* Trick phones to connect → attacker can capture location, calls, texts, etc.

---

## 🔹 Expanded Writeup

### 1. Finding IMEI & IMSI Yourself

* **IMEI:** Dial `*#06#`, check in Settings → About Phone, or printed on SIM tray/device.
* **IMSI:** Visible in SIM Status on some Androids or through SIM info apps.

### 2. Can IMEI/IMSI Alone Track a Device?

* **IMEI** → Used to blacklist stolen phones.
* **IMSI** → Used by carriers to know which tower your SIM is connected to.
* Neither can be used by a normal user for tracking; only carriers/police can.

### 3. How Carriers & Police Trace Devices

* **Cell tower triangulation**: Estimates location by comparing signals from towers.
* **Database lookups**: Maps IMSI/IMEI to tower connections.
* **IMSI catchers (StingRays)**: Fake towers trick phones, accuracy within tens of meters.
* **GPS access (via Google/Apple)**: Most precise, within 5–10 meters.

### 4. IP vs Carrier Tracking

* **IP Tracking**: Shows only the approximate city/region (accuracy in kilometers).
* **Carrier Tracking**: Much closer to real location, typically 20 m – 2 km.

### 5. Normal User vs Hacker vs Authorities

* **Normal User:**

  * Android → Google Find My Device (needs Gmail logged in).
  * iPhone → iCloud Find My iPhone (needs iCloud account access).
  * Tablets → Specific apps (Hangouts, Google account apps).

* **Authorities:**

  * Can directly trace or block devices using IMSI/IMEI & cell tower logs.

* **Hackers:**

  * Advanced techniques: SS7 exploitation, IMSI catchers, spyware like Pegasus.
  * These allow location tracking, interception, and session data leaks.


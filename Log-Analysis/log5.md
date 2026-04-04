# OSI Model & Traffic Analysis

## 📌 Overview
Today’s focus was on the backbone of network communication: the **OSI (Open Systems Interconnection) Model**. Understanding these seven layers is critical for security log analysis because it allows us to isolate where an issue or an attack is occurring.


## 🏗️ The 7 Layers of the OSI Model
The OSI model is a conceptual framework that standardizes how different computer systems talk to each other.

### **The "Upper" Layers (Data Handling)**
* **Layer 7: Application** – The interface where the user interacts with the network (e.g., HTTP for web browsing, SMTP for email).
* **Layer 6: Presentation** – The "translator." It handles data encryption, compression, and formatting (e.g., converting a JPG or encrypting an SSL/TLS session).
* **Layer 5: Session** – The "manager." It opens, maintains, and closes the communication session between two devices, using checkpoints to prevent data loss.

### **The "Heart" of Log Analysis (The Focus Layers)**
* **Layer 4: Transport (TCP/UDP)**
    * **Unit:** Segments.
    * **Function:** Handles end-to-end communication, flow control, and error correction.
    * **Analysis Tip:** This is where we see the **TCP Three-Way Handshake**.
* **Layer 3: Network (IP)**
    * **Unit:** Packets.
    * **Function:** Routing data between different networks. It finds the best physical path for the data.
* **Layer 2: Data Link**
    * **Unit:** Frames.
    * **Function:** Transfers data between two devices on the *same* network.
* **Layer 1: Physical**
    * **Unit:** Bits (1s and 0s).
    * **Function:** The actual hardware—cables, switches, and radio waves.

---

## 🔄 How Data Travels: Encapsulation
To understand logs, I learned that data flows like a "Russian Nesting Doll":
1.  **Sending:** Data starts at Layer 7 and travels down, getting wrapped in headers at each layer (Data → Segment → Packet → Frame → Bits).
2.  **Receiving:** The receiving device "unwraps" the headers starting from the bottom up to the application layer.

---

## 🛠️ Lab Practice: Wireshark & The Three-Way Handshake
In cybersecurity, Layer 4 is where we often detect "SYN Floods" or connection issues. I used Wireshark to observe the **TCP Three-Way Handshake**, which follows this logic:

1.  **SYN** (Synchronize): The client asks to connect.
2.  **SYN-ACK** (Synchronize-Acknowledge): The server says "I'm here, let's talk."
3.  **ACK** (Acknowledge): The client says "Got it, let's start."

**Wireshark Filter used:** `tcp.flags.syn==1`



---

## 🛡️ Why This Matters for Security
* **Targeted Attacks:** Application layer attacks (Layer 7) target things like web forms, while Protocol attacks (Layers 3 & 4) try to overwhelm the network's ability to process connections.
* **Troubleshooting:** If I can see a "SYN" packet in the log but no "SYN-ACK," I know the problem is at the Transport layer (Layer 4) or the server is down, saving me from wasting time checking the physical cables (Layer 1).

---

## 🧠 Key Takeaway
The OSI model isn't just a theoretical map; it's a **diagnostic tool**. In log analysis, knowing which layer a log entry belongs to tells you exactly what part of the communication chain is failing or under attack.

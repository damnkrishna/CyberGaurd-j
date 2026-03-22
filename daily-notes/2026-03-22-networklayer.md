# Transport Layer Notes (Flow & Congestion Control)

---

## 1. Error Control

### Purpose

* Detect and correct errors during data transmission

### Techniques

* **Checksum**: Error detection
* **Acknowledgment (ACK)**: Confirms receipt
* **Timeout**: Detects lost packets

---

### Types of Acknowledgment

* **Cumulative ACK**

  * Acknowledges all packets up to a certain sequence number

* **Selective ACK (SACK)**

  * Acknowledges specific packets individually

---

### RTT (Round Trip Time)

* Time taken for a packet to travel from sender to receiver and back

---

**Note**

* Lost ACKs may create deadlock if not handled properly

---

## 2. Congestion Control

### Purpose

* Detect and reduce network congestion

---

### Key Concepts

* **Congestion Window (cwnd)**: Sender-side control
* **Congestion Policy**: Rules to manage congestion

---

### Performance Metrics

* Delay
* Throughput

---

### Types of Congestion Control

#### Open Loop (Prevention)

* Prevent congestion before it occurs

#### Closed Loop (Removal)

* Detect and correct congestion after it occurs

---

### Window Sizes

Sender maintains:

* **Receiver Window (rwnd)**: Advertised by receiver
* **Congestion Window (cwnd)**: Managed by sender

**Actual Window Size**

```
min(rwnd, cwnd)
```

---

## 3. TCP Congestion Control Algorithms

---

### Slow Start

* cwnd increases exponentially
* Continues until threshold (**ssthresh**) is reached

---

### Additive Increase

* After threshold is reached:

  * cwnd increases linearly
  * Approximately 1 MSS per ACK

* Continues until congestion is detected

---

### Multiplicative Decrease

When congestion occurs:

* **Timeout detected**

  * Restart Slow Start

* **3 duplicate ACKs**

  * Enter Congestion Avoidance

---

## 4. TCP Variants

---

### TCP Tahoe

* cwnd starts at 1 MSS
* Uses:

  * Slow Start
  * AIMD (Additive Increase, Multiplicative Decrease)
  * Fast Retransmit

---

### TCP Reno

* Enhancement over Tahoe

* Adds:

  * Fast Recovery

* Behavior:

  * cwnd is reduced (not reset completely)
  * Then grows linearly

---

## 5. Fast Retransmit and Recovery

### Trigger

* 3 duplicate ACKs

### Actions

* Retransmit lost packet immediately
* Skip slow start
* Enter Fast Recovery

---

### Fast Recovery Logic

* Threshold = cwnd / 2
* cwnd = threshold
* Then increases linearly per ACK

---

## 6. TCP Timers

---

### Types of Timers

* **Retransmission Timer**

  * Retransmits packets after timeout

* **Persistence Timer**

  * Prevents deadlock in zero-window situations

* **Keepalive Timer**

  * Detects inactive connections

* **Time-Wait Timer**

  * Used during connection termination

---

## 7. Flow Control Mechanisms

---

### Stop and Wait

**Working**

* Sender sends one frame and waits for ACK before sending the next

**Limitation**

* Very low efficiency due to idle time

---

### Go-Back-N (GBN)

**Working**

* Sender sends multiple frames without waiting
* If one frame is lost:

  * Receiver discards subsequent frames
  * Sender retransmits from the lost frame onward

**Example**

```
Send: 1, 2, 3, 4
If 2 is lost:
Receiver discards 3, 4
Sender resends 2, 3, 4
```

**Limitation**

* Wastes bandwidth due to retransmission of correct frames

---

### Selective Repeat (SR)

**Working**

* Only lost frames are retransmitted

**Example**

```
Send: 1, 2, 3, 4
If 2 is lost:
Receiver stores 3, 4
Sender resends only 2
```

**Limitations**

* More complex
* Requires buffer at receiver

---

## 8. Window Size Comparison

| Protocol         | Sender Window | Receiver Window |
| ---------------- | ------------- | --------------- |
| Stop and Wait    | 1             | 1               |
| Go-Back-N        | 2ⁿ − 1        | 1               |
| Selective Repeat | 2ⁿ⁻¹          | 2ⁿ⁻¹            |

---

## Quick Summary

* Error Control: Checksum, ACK, Timeout
* Flow Control: Stop and Wait, Go-Back-N, Selective Repeat
* Congestion Control: Uses cwnd and control algorithms
* Actual Window Size: min(rwnd, cwnd)
* TCP Tahoe: Basic model
* TCP Reno: Adds Fast Recovery

---

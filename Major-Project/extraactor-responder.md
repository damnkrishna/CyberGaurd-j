# Aegis Notes: Logging, eBPF, and Runtime Security

## Part 1: Why Loki Matters for Aegis (LLM Integration)

Metrics (like CPU spikes or HTTP 500 rates) tell you that a system is broken. Traces tell you where it is broken. But logs tell you the story of why it broke.

For an LLM-powered assistant or auto-remediation tool like Aegis, context is everything. If a checkout service fails, Aegis needs to read the exact sequence of events (e.g., a database connection timeout followed by a failed retry loop) to understand the failure. Loki acts as the high-speed library for this context, allowing Aegis to dynamically query and retrieve the exact "story" of an incident so the LLM can analyze it.

### Core Concepts to Master

#### 1. Labels: How Loki Organizes Chaos

Loki borrows its labeling system directly from Prometheus. Instead of storing logs in massive, unstructured buckets, Loki groups them into streams defined by labels (key-value pairs).

**Example labels:** `env="prod"`, `app="checkout"`, `namespace="payment-gateway"`

Every unique combination of labels creates a new log stream. When you query Loki, you always start by selecting these labels to narrow down the haystack before searching for the needle.

#### 2. LogQL: Loki's Query Language

LogQL is how you extract insights from Loki. It feels like writing a Prometheus query, followed by a series of Unix pipeline commands (like `grep` or `awk`).

A standard LogQL query has two parts:

- **Log Stream Selector** — finds the right logs using labels. Example: `{app="checkout", env="prod"}`
- **Log Pipeline** — filters, parses, and formats the log lines within that stream. Example: `|= "error"` (contains the word "error").

**Combined example:**

```logql
{app="checkout", env="prod"} |= "error" != "timeout" | json | latency > 500
```

Translation: "Find all logs for the production checkout app, filter for lines containing 'error' but NOT 'timeout', parse the JSON, and only show me lines where the 'latency' field is greater than 500."

#### 3. Promtail: The Log Shipper

Loki doesn't collect logs itself — it just stores them. Promtail is the agent you deploy on your servers or Kubernetes nodes.

- **Discovery** — Promtail automatically discovers targets (like Kubernetes pods).
- **Labeling** — it attaches standard labels to the logs based on where they came from (e.g., tagging a log with the pod name it originated from).
- **Shipping** — it tails the log files and ships them to the centralized Loki server over HTTP.

#### 4. Structured vs. Unstructured Logs

- **Unstructured logs** — plain text (e.g., `2023-10-25 INFO Checkout failed for user 123`). To extract "user 123" in LogQL, you have to write complex regex.
- **Structured logs (JSON)** — logs output as JSON objects (e.g., `{"level":"info", "msg":"Checkout failed", "user_id": 123}`).

**Why JSON wins:** LogQL has native parsing pipelines (like `| json`). If you send JSON logs to Loki, you don't need to pre-index the fields — you can parse them at query time, immediately turning JSON keys into queryable labels.

#### 5. Log Streaming via Grafana

Grafana acts as the UI for Loki. Because Loki shares Prometheus's label structure, Grafana allows you to seamlessly correlate metrics and logs. If you see a spike on a Grafana metric dashboard, you can instantly pivot to a live stream of the logs that share those exact same labels, viewing the log lines in real time as they stream in.

---

## Part 2: eBPF and Falco for Aegis-SRE

### 1. What Are eBPF and Falco?

#### 🐝 eBPF (extended Berkeley Packet Filter)

Think of eBPF as a "safe runtime / sandbox running directly inside the Linux kernel."

- **The problem:** Traditionally, if you wanted to monitor low-level OS operations (like when a process opens a file, spawns a process, or opens a network socket), you had to write custom Linux kernel modules (risky — a single bug can panic the whole kernel) or use user-space tracing tools like `strace` (extremely slow).
- **The eBPF solution:** eBPF allows tiny, sandboxed bytecode programs to run inside the Linux kernel at specific event hook points (syscall entry/exit, tracepoints, socket operations) without modifying kernel source code.
- **Why it's special:** The kernel runs a strict **verifier** on eBPF code before loading it, guaranteeing it will never crash the kernel, deadlock, or leak memory.

#### 🦅 Falco

Falco is an open-source, CNCF-graduated **runtime security monitoring tool** that uses eBPF under the hood.

- **Mental model:** If **Prometheus** is a thermometer measuring CPU/RAM heat, **Falco** is a security camera watching for lock-pickers.
- **How it works:** Falco hooks into Linux kernel system calls (`execve`, `openat`, `connect`, `ptrace`, etc.) using an eBPF probe. It compares every syscall against declarative **Falco Rules** (written in YAML).
- **What it outputs:** When a suspicious rule triggers (e.g., someone spawning `/bin/bash` inside a container or reading `/etc/shadow`), Falco generates structured **JSON security alerts** packed with context:
  - Process details (`proc.cmdline`, `proc.pname`, `user.name`)
  - Container metadata (`container.id`, `k8s.pod.name`, `k8s.ns`)
  - System call details (`fd.name`, `evt.type`)

### 2. How Tough Will Making These Connections Be?

The good news for **Aegis-SRE**: **you do NOT need to write raw C/eBPF code from scratch!** Falco and Cilium do the heavy eBPF lifting in kernel-space. Your task is to connect the telemetry streams and orchestration logic.

Here is the breakdown of the four connection points:

#### 🟢 Connection 1: Falco Deployment in K3s (Difficulty: Easy to Moderate)

- **What to do:** Install Falco on your K3s cluster (Oracle ARM A1) using the official Helm chart with `driver.kind=ebpf`.
- **Why it's manageable:** The Helm chart automates installing Falco as a DaemonSet across your cluster.
- **Gotchas:** Ensure your Linux kernel on Oracle ARM has eBPF/BTF (BPF Type Format) enabled (standard on modern Ubuntu/Debian kernels).

#### 🟢 Connection 2: Falco Alert Stream → Aegis Event Pipeline (Difficulty: Easy)

- **What to do:** Forward Falco alerts into your system using either:
  - **Option A:** `Falcosidekick` (an official Falco plugin) sending HTTP POST webhooks directly to your Aegis backend/Go service.
  - **Option B:** Promtail picking up standard stdout/file logs from `/var/log/falco.log` and sending them to Loki.
- **Why it's easy:** Falco outputs clean, standard JSON out of the box! You don't have to parse raw eBPF binary buffers — Falco has already translated the kernel events into key-value pairs like `%k8s.pod.name` and `%proc.cmdline`.

#### 🟡 Connection 3: Falco Alert → LLM Diagnostic Engine (Difficulty: Moderate)

- **What to do:** When an alert arrives (e.g., `Shell Spawned in Container`), extract key fields and feed them into your Ollama (Llama 3.1 8B) prompt alongside recent logs from Loki and MITRE TTP runbooks from your vector DB (RAG).
- **Why it's moderate:** Requires prompt engineering and strict JSON output formatting so the LLM outputs a clean classification object:

  ```json
  {
    "category": "ATTACK",
    "action": "QUARANTINE",
    "target": "checkout-service-pod-xyz",
    "reason": "MITRE T1059: Shell spawned in pod"
  }
  ```

#### 🟡 Connection 4: Aegis Decision → Cilium eBPF Quarantine (Difficulty: Moderate)

- **What to do:** When the LLM and guardrail classify an incident as an **ATTACK**, the Go controller applies a `CiliumNetworkPolicy` to isolate the target pod.
- **Why it works so well:** Cilium enforces network rules at the eBPF socket layer, dropping all ingress/egress traffic instantly without iptables overhead.
- **Why it's moderate:** This relies on standard Kubernetes API operations via `client-go` or `kubectl apply`, but you need to test that the attacker pod is caged without accidentally breaking surrounding healthy microservices.

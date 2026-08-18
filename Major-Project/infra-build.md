# ☁️ Aegis-SRE: Phase 1 — Cloud Infrastructure Setup & Engineering Guide

> **Goal:** Step-by-step guide to provisioning a $0/month Always Free Oracle Cloud ARM Kubernetes cluster for Aegis-SRE with complete zero-downtime firewall, SSH, and eBPF configuration.

---

## 📋 Prerequisites & Hardware Allocation

| Cloud Resource | Provider | Specs | Cost |
|---|---|---|---|
| **Cluster Host** | Oracle Cloud Infrastructure (OCI) | `VM.Standard.A1.Flex` (4 OCPU, 24 GB RAM, Ubuntu 22.04 LTS ARM64, 200 GB Storage) | **$0 / month** (Always Free) |
| **Kubernetes Distro** | K3s (Lightweight K8s) | Enterprise-grade K8s optimized for ARM64 | **$0** |

### 📊 Cloud RAM Allocation Budget (24 GB Total)
* **K3s Control Plane + Target Microservices (Online Boutique):** ~3.5 GB RAM
* **Observability Sensors (Prometheus + Loki + Falco eBPF):** ~3.5 GB RAM
* **Diagnostic AI Brain (Ollama Llama 3.1 8B Q4):** ~5.5 GB RAM
* **Available Headroom:** ~11.5 GB RAM (50% Safety Margin) 🟢

---

## 🛠️ Step 1: Provision Oracle Cloud ARM Instance

1. Sign up / log into your **Oracle Cloud Always Free** account at [oracle.com/cloud/free](https://www.oracle.com/cloud/free/).
2. In the Oracle Console, go to **Compute ➔ Instances ➔ Create Instance**.
3. Configure the VM parameters:
   * **Name:** `aegis-k3s-node-1`
   * **Image:** `Ubuntu 22.04 LTS` (Select ARM64 architecture)
   * **Shape:** `Ampere` ➔ `VM.Standard.A1.Flex`
   * **OCPU Count:** `4 OCPU`
   * **Memory:** `24 GB RAM`
   * **Networking:** Default VCN & Public Subnet (Assign a public IPv4 address)
   * **SSH Keys:** Save the generated SSH Private Key file (`oracle_key.key`) to your computer.
   * **Boot Volume:** 100 GB or 200 GB (Free Tier limit)
4. Click **Create** and wait for instance status to turn **Running** 🟢.

---

## 🔐 Step 2: Configure Oracle Cloud VCN Security List & Linux Firewall

### A. Oracle Cloud Console Ingress Rules
In Oracle Cloud Console, navigate to **Networking ➔ Virtual Cloud Networks ➔ Default Security List for VCN** and add these **Ingress Rules**:

| Source CIDR | Protocol | Port Range | Purpose |
|---|---|---|---|
| `0.0.0.0/0` | TCP | `22` | SSH Terminal Access |
| `0.0.0.0/0` | TCP | `6443` | Kubernetes K3s API Server |
| `0.0.0.0/0` | TCP | `80`, `443` | Public HTTP/HTTPS Web Ingress |
| `0.0.0.0/0` | TCP | `3000` | Grafana Command Center |

### B. Oracle Ubuntu OS `iptables` Flush (Engineering Recommendation)
By default, Oracle Cloud Ubuntu images include strict `iptables` rules that block incoming traffic on non-standard ports. Run these commands inside your VM to open traffic cleanly:

```bash
# Flush default OCI iptables restrictions
sudo iptables -F
sudo netfilter-persistent save
```

---

## 🚀 Step 3: Connect via SSH & Install K3s

From your local machine terminal / PowerShell, connect to your Oracle VM:

```bash
ssh -i path/to/oracle_key.key ubuntu@<YOUR_ORACLE_PUBLIC_IP>
```

> **💡 Engineering Recommendation (SSH Keep-Alive):**
> To prevent your SSH terminal from freezing or timing out when idle, add `ServerAliveInterval 60` to your local SSH config (`~/.ssh/config`).

Once connected inside the Oracle VM shell, run the single-command K3s installer:

```bash
# 1. Install K3s Kubernetes
curl -sfL https://get.k3s.io | sh -

# 2. Allow non-root kubectl access
sudo chmod 644 /etc/rancher/k3s/k3s.yaml

# 3. Verify K3s Cluster Node is healthy
kubectl get nodes -o wide
```

---

## 💻 Step 4: Connect Local Machine `kubectl` to Cloud K3s

To manage the Cloud K3s cluster directly from your workspace without filling local PC memory/disk:

1. Copy `/etc/rancher/k3s/k3s.yaml` from your Oracle VM to your local PC.
2. Edit the copied `k3s.yaml` file and replace `127.0.0.1` with `<YOUR_ORACLE_PUBLIC_IP>`.
3. Set your local environment variable:
   * **PowerShell:** `$env:KUBECONFIG="C:\path\to\cloud-k3s.yaml"`
   * **Linux/Mac:** `export KUBECONFIG=~/cloud-k3s.yaml`
4. Run `kubectl get nodes` on your local PC — you will see your **Oracle ARM Cloud Cluster** respond!

---

## 🔧 Step 5: eBPF & Kernel Verification Checklist

Before deploying Falco, verify that eBPF and BTF tracepoints are active on the cloud VM:

```bash
# Verify kernel version (Must be >= 5.15)
uname -r

# Verify BTF vmlinux support is enabled for eBPF
ls -la /sys/kernel/btf/vmlinux
```

---

## 🎯 Step 6: Deploy Phase 1 Manifests

Once the cloud cluster responds to `kubectl`, we will deploy Phase 1 manifests directly to the cloud:

```bash
# Deploy target microservices & chaos pods directly to cloud
kubectl apply -f k8s/00-namespace.yaml
kubectl apply -f k8s/online-boutique/
kubectl apply -f k8s/chaos/
```

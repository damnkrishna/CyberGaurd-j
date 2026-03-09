# FedShield: Privacy-Preserving Federated Malware Detection

## Abstract

FedShield is a privacy-preserving federated malware detection system that enables organizations to collaborate on cybersecurity intelligence without sharing raw data. Traditional centralized systems require uploading executable files or logs to a central server, creating risks related to privacy, intellectual property, and data confidentiality.

FedShield solves this using Federated Learning (FL), where distributed clients train a shared model locally and send only model updates to a central server instead of raw data.

To strengthen security, the system integrates Secure Aggregation (via Diffie–Hellman key exchange) and Differential Privacy, which masks individual updates and adds Laplacian noise to prevent data reconstruction.

The prototype uses the EMBER 2024 malware dataset with 524-dimensional PE features and evaluates performance under Non-IID data distributions using Dirichlet (α=0.1) and Shard partitioning. While isolated models drop from 85% to 60% accuracy, FedShield maintains a 20% resilience advantage, demonstrating that federated learning improves robustness while preserving data privacy in collaborative malware detection.

---

## 1. Introduction

Malware detection plays a crucial role in protecting computer systems, enterprise infrastructures, and digital services from increasingly sophisticated cyber threats. Machine learning techniques have significantly improved malware detection by enabling automated identification of malicious software patterns from large datasets.

Traditional malware detection systems rely on centralized architectures in which executable files or extracted features are collected and processed on a central server. Although centralized learning can produce accurate detection models, it introduces several challenges including privacy risks, scalability limitations, and concerns regarding data ownership.

Organizations such as financial institutions, hospitals, and technology companies often possess sensitive or proprietary software that cannot be shared externally due to regulatory or confidentiality constraints (GDPR, HIPAA). Uploading such data to centralized servers may expose intellectual property or confidential internal information.

Federated Learning provides an alternative paradigm where multiple participants collaboratively train a shared machine learning model without transferring raw data. Each participant trains the model locally and shares only model updates with a central aggregation server.

FedShield applies federated learning techniques to malware detection while integrating secure aggregation and differential privacy mechanisms to ensure privacy-preserving collaborative model training. The system extends the academic PrivacyFL framework (Mugunthan et al., ACM CCS 2020) with Non-IID robustness validation, comprehensive benchmarking, and modern dataset support.

---

## 2. Methodology

The FedShield system follows a federated learning workflow consisting of data preparation, local model training, privacy protection mechanisms, and global model aggregation.

### 2.1 Dataset

The EMBER 2024 (Elastic Malware Benchmark for Empowering Researchers) dataset is used for training and evaluation.

| Property | Value |
|---|---|
| Source | HuggingFace Hub (joyce8/EMBER2024) |
| Format | .jsonl (PE file metadata) |
| Feature Dimensions | 524 continuous features |
| Features Include | Byte histogram, entropy, string stats, PE headers, imports |
| Training Pool | 7,500 samples (Sept 2023 – Sept 2024) |
| Test Pool | 2,000 samples (Sept 2024 – Dec 2024) |
| Classes | Binary: 0 (Benign), 1 (Malware) |

**Temporal Generalization:** Training and test data are split chronologically, not randomly. The model trains on 2023-era malware and is tested on completely unseen late-2024 malware, validating real-world viability against evolving threats.

### 2.2 Federated Learning Workflow

The federated training process consists of multiple communication rounds between a central server and distributed clients.

During each round:

1. The server distributes the current global model to all clients.
2. Each client performs local training using its private dataset.
3. Clients compute updated model parameters.
4. Differential Privacy noise is injected into the weights (Laplacian, ε-bounded).
5. Diffie-Hellman cryptographic masks are applied to the noised weights.
6. Clients send the protected, masked updates to the server.
7. The server aggregates updates using the Federated Averaging (FedAvg) algorithm (DH masks cancel automatically upon summation).
8. The updated global model is redistributed to all clients.

This process repeats for 5 iterations until the model converges.

### 2.3 Local Model Training

Local training is performed using a Logistic Regression classifier implemented with the `SGDClassifier` algorithm from the Scikit-learn library. The model uses the `partial_fit(classes=[0, 1])` method, which:

- Supports incremental learning across federated rounds
- Explicitly declares the full class set, preventing crashes on single-class batches under Non-IID
- Works identically for both IID and Non-IID scenarios

### 2.4 Privacy Protection Mechanisms

Two privacy-preserving mechanisms are incorporated:

**Secure Aggregation (Diffie-Hellman):** Before training begins, every pair of clients performs a Diffie-Hellman key exchange to agree on a shared secret s_an. Client A adds +s_an to its weights; Client B adds −s_an. When the server sums all masked weights:

```
(w_a + s_an) + (w_n − s_an) = w_a + w_n
```

The mask vanishes. The server never sees individual w_a or w_n.

**Differential Privacy (Laplacian Noise):** Before any weight leaves a client, calibrated Laplacian noise is injected, scaled by the sensitivity and privacy budget ε (epsilon). At ε=1.0, the noise is small enough to preserve accuracy (~0.1% drop) while making reconstruction attacks mathematically infeasible.

### 2.5 Non-IID Data Partitioning

Two research-standard partitioning algorithms are implemented (validated against the Blades benchmark):

- **Dirichlet Partitioning (α=0.1) — Prior Probability Shift:** Each client's label proportion is drawn from Dir(α). At α=0.1, distributions are extremely concentrated — one client gets 99.7% malware (3,723 out of 3,733 samples), another gets 99.7% benign.

- **Shard Partitioning (2 shards/client) — Concept Shift:** Data is sorted by label, divided into 6 equal shards, and 2 shards are randomly assigned per client. Creates hard label concentration where a client may see predominantly one class.

---

## 3. System Architecture

*(Architecture diagram)*

---

## 4. Results and Observations

### 4.1 Experiment 1: Differential Privacy Impact Assessment (IID)

Under balanced (IID) data, we test 4 configurations to measure the cost of privacy:

| Configuration | Accuracy | Precision | Recall | F1-Score |
|---|---|---|---|---|
| No DP (raw gradients) | 85.50% | 87.06% | 81.56% | 84.22% |
| DP — Gamma (ε=1.0) | 85.50% | 87.06% | 81.56% | 84.22% |
| DP — Laplace (ε=1.0) | 85.40% | 86.87% | 81.56% | 84.13% |
| Client Dropout (tolerance=10) | 84.00% | 85.06% | 80.40% | 82.67% |

**Confusion Matrix (Baseline — No DP)**

| | Pred=Benign | Pred=Malware |
|---|---|---|
| **True=Benign** | 936 | 115 (89.06% correct) |
| **True=Malware** | 175 | 774 (81.56% correct) |

**Observations:**

- DP at ε=1.0 has negligible impact on performance. Gamma noise produces identical results; Laplace reduces accuracy by only 0.1%.
- 175 malware samples are missed (false negatives) — the model is slightly conservative.
- Client dropout degrades accuracy by only 1.5%, demonstrating graceful degradation when clients go offline.

### 4.2 Experiment 2: Non-IID Data Distribution (Core Contribution)

**Training Data Distribution per Client**

| Client | IID (Balanced) | Dirichlet α=0.1 | Shard (2/client) |
|---|---|---|---|
| Client 0 | 3,831 / 3,669 | 27 benign, 10 malware | 1,256 / 1,244 |
| Client 1 | 3,672 / 3,828 | 10 benign, 3,723 malware | 10 / 2,500 |
| Client 2 | 3,831 / 3,669 | 3,719 benign, 11 malware | 2,500 / 10 |

Under Dirichlet α=0.1, Client 1 receives 99.7% malware and Client 2 receives 99.7% benign — simulating real-world institutional bias where a financial institution encounters mainly ransomware while a home ISP encounters mainly benign traffic.

**Headline Results: Silo vs FedShield**

| Experiment | Silo (Isolated Avg) | FedShield (Federated) | Resilience Gap |
|---|---|---|---|
| IID (balanced) | 85.12% | 85.45% | +0.33% |
| Dirichlet α=0.1 | 60.07% | 80.10% | +20.03% |
| Shard (2/client) | 61.58% | 80.25% | +18.67% |

> **Key Finding:** Isolated silo models collapse by 25 percentage points under Non-IID, while FedShield only drops ~5 points. The **+20% resilience gap** is the core academic contribution.

**FedShield Federated — Dirichlet α=0.1**

| Metric | Value |
|---|---|
| Accuracy | 80.10% |
| Precision | 79.40% |
| Recall | 78.40% |
| F1-Score | 78.90% |

**FedShield Federated — Shard (2/client)**

| Metric | Value |
|---|---|
| Accuracy | 80.25% |
| Precision | 90.86% |
| Recall | 64.91% |
| F1-Score | 75.72% |

**Silo Collapse Analysis — Why Isolated Models Fail**

Under Dirichlet α=0.1:

| Client | Accuracy | Precision | Recall | F1 | TN | FP | FN | TP | Diagnosis |
|---|---|---|---|---|---|---|---|---|---|
| Client 0 | 79.70 | 87.24 | 67.02 | 75.80 | 958 | 93 | 313 | 636 | Reasonable (tiny but mixed data) |
| Client 1 | 47.60 | 47.52 | 100 | 64.43 | 3 | 1,048 | 0 | 949 | Labels EVERYTHING as malware |
| Client 2 | 52.90 | 100 | 0.74 | 1.46 | 1,051 | 0 | 942 | 7 | Labels EVERYTHING as benign |

- **Client 1** (99.7% malware data): Learned to scream "VIRUS!" at everything. It flags all 1,051 benign files as malware (FP=1,048). Only 3 benign files were correctly identified.
- **Client 2** (99.7% benign data): Learned to say "Safe!" to everything. It catches only 7 out of 949 actual malware samples (TP=7). 942 real viruses pass through undetected — a catastrophic security failure.
- **FedShield Federated:** Despite being built from these broken clients' encrypted gradients, the federated model catches 744 out of 949 malware with only 193 false alarms, by implicitly combining Client 1's malware gradient knowledge with Client 2's benign pattern knowledge.

**Under Shard Partitioning — Even More Extreme**

| Client | Accuracy | TN | FP | FN | TP | F1 | Diagnosis |
|---|---|---|---|---|---|---|---|
| Client 0 | 84.75 | 938 | 113 | 192 | 757 | 83.23 | Balanced shards |
| Client 1 | 47.40 | 0 | 1,051 | 1 | 948 | 64.31 | TN=0: Cannot identify ANY benign file |
| Client 2 | 52.60 | 1,051 | 0 | 948 | 1 | 0.21 | TP=1: Catches ONE malware out of 949 |

**Convergence Analysis**

The federated model converges within 2–3 rounds under all conditions. Under IID, accuracy stabilizes at ~85%. Under Non-IID, the model fluctuates due to conflicting gradient signals from biased clients but consistently stays 15–20 percentage points above the silo baseline throughout all 5 iterations.

---

## 5. Impact and Applications

The FedShield framework demonstrates a scalable and privacy-preserving approach for collaborative cybersecurity defense.

The system enables multiple organizations to collectively improve malware detection models without sharing sensitive executable files or internal data. The +20% resilience gap under Non-IID proves that federation is not optional — it is essential when institutions have biased local data.

Potential applications include:

- **Enterprise Cybersecurity Platforms:** Banks, hospitals, and corporations collaborating on threat detection without sharing proprietary network data.
- **Financial Sector Threat Detection:** Cross-bank ransomware detection while maintaining regulatory compliance (PCI-DSS, GDPR).
- **Healthcare Infrastructure Protection:** Hospitals sharing malware intelligence without exposing patient record metadata.
- **Government Cybersecurity Networks:** Inter-agency threat intelligence sharing across classified boundaries.
- **Collaborative Threat Intelligence Platforms:** Multi-vendor antivirus consortium training without revealing signature databases.

---

## 6. Future Work

| Enhancement | Description | Expected Impact |
|---|---|---|
| Deep Learning Swap | Replace SGDClassifier with PyTorch multi-layer neural networks | 85% → 94%+ accuracy |
| Byzantine Attack Defense | Implement Label-Flipping, ALIE attacks with MultiKrum/TrimmedMean defenses | Robustness against malicious clients |
| Serverless Mesh Topology | Eliminate central server; clients compute FedAvg peer-to-peer | No single point of failure |
| Upgraded Cryptography | Integrate ElGamal/ECC encryption | Stronger cryptographic guarantees |
| Cross-Dataset Validation | Add Android (Drebin) and IoT (IoT-23) datasets | Prove architecture is data-agnostic |
| Adaptive DP | Dynamic ε adjustment based on convergence | Better privacy-accuracy tradeoff |
| Containerized Deployment | Docker containers with REST API communication | Production-ready system |

---

## 7. References

1. McMahan, H. B., Moore, E., Ramage, D., Hampson, S., Arcas, B. A. "Communication-Efficient Learning of Deep Networks from Decentralized Data." *AISTATS 2017.*

2. Anderson, H., Roth, P. "EMBER: An Open Dataset for Training Static PE Malware Machine Learning Models." *ArXiv 2018.* Updated: EMBER 2024.

3. Kairouz, P., McMahan, H. B., et al. "Advances and Open Problems in Federated Learning." *Foundations and Trends 2021.*

4. Mugunthan, V., Peraire-Bueno, A., Kagal, L. "PrivacyFL: A Simulator for Privacy-Preserving and Secure Federated Learning." *ACM SIGSAC CCS 2020.*

5. Li, S., et al. "Blades: A Unified Benchmark Suite for Byzantine Attacks and Defenses in Federated Learning." *IEEE IoTDI 2024.*

6. Priyanshu, A. "Federated-Learning — Non-IID taxonomy and implementations." GitHub Repository.

7. Pham, X. S. "Secure-Federated-Learning — ECC and ElGamal integration." GitHub Repository.

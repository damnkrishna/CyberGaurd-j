# Federated Learning

## What is Federated Learning?

The basic idea of federated learning is to create a mechanism where several computers, instead of sharing their local data, just share the maths or reports of the data to protect confidential data and improve privacy.

This concept was first introduced in 2016 by a Google employee. Later, as it was seen as very good and very helpful in saving company data, it was added in industries and projects to create a more secure mechanism for data transfer and security.

I didn't know federated learning is itself a big field, not just an upgrade from centralized to federated. Inside federated learning too, there are several methods to improve the balance between privacy, communication efficiency, and computation cost.

<img width="641" height="259" alt="Screenshot 2026-02-05 091319" src="https://github.com/user-attachments/assets/206048b4-5be2-4ef2-b9e1-865f076527aa" />

## How It Works

Basically, in federated learning, the main goal is to train computers locally on several computers individually. They can change some code or use custom data and subsequently send the update to the server, which combines the updates and produces a global improved model.

This is all because some countries have very strict data or privacy protection rules, which result in lesser trust on centralized models—hence the uprising of federated learning models.

So FL is a setup to train models locally, then use all the model feature data that is important to train a main federated model. The work involves setting the weightage of client data shared to the federated model and the final training to improve the central model. Basically, we decide what share and weightage the value or data coming from a certain client will have in the final model and improvement, and based upon all this stuff, we build a federated learning model.

## The Steps

1. **Client Selection**: The server keeps track of potential client₁ to clientₙ, which are usually edge servers, IoT devices, or smartphones. The server chooses k node clients from a collection of clients that satisfy the requirements for the FL process.

2. **Broadcasting**: A machine learning model called model M is initialized on the server. Weights and biases in the model are established via random initialization or through pre-training with the available global dataset. This initial model M is sent to every selected client by the server.

3. **Client Local Training**: Among the k clients chosen by the server, each clientᵢ, where 1 ≤ i ≤ n, will use its local data to train the initial model locally. It will then use the gradient descent technique to optimize the learning model, encrypt it, and share the updated model with the server.

4. **Aggregation**: The local model updates are gathered by the server from the k clients, validated, and the lagging updates are removed and then aggregated to create the global model M_FED.

5. **Model Update**: For the current round j, the cumulative update Uⱼ of k clients is compiled and distributed to the chosen clients in the subsequent round as the global model. Steps 3 to 5 are repeated until the loss function reaches convergence.

## Classification of FL
<img width="641" height="259" alt="Screenshot 2026-02-05 094409" src="https://github.com/user-attachments/assets/4c59d1bd-32c8-41f0-8ebd-66f4ee1876f8" />

### 1. Centralized

One central computer controls all—we set the weight of client data usage and its importance in the final model trained. That central entity server thing.

As a matter of fact, I think this is what antiviruses like McAfee and others do because they take our whole file and analyze it centrally and then give final updates to all computers, sharing it to all connected models like new updates or something internally.

And that's what I don't wanna build because someone already is doing it. I wanna do something different, so I will go with decentralized.

### 2. Decentralized

It refers to when no computer holds the absolute power of deciding weightage and all in a model's final training or giving final updates to all models internally.

I think it must work like this: if my computer learns something new and it is verified by the model, then instead of asking for permission or getting verified by a central model, it will share what it learned to others.

## Federation Scale

FL systems fall into two categories based on the federation scale:

**Cross-device**: FL systems consist of numerous mobile devices with diverse processing capabilities, where the model is distributed to the clients and trained on local data during the training phase.

**Cross-silo**: The number of federated clients is often low, but their computing capacity is high, typically found in large enterprises or data centers. In this, the local model is combined with data centers and data silos to create a global model.

## Data Distribution Types

FL is divided into three types based on how data is distributed across the sample and feature spaces:

**Horizontal Federated Learning**: Datasets are split horizontally based on the user dimension, and the part of the datasets that has similar user attributes but differs in users is considered for training.

**Vertical Federated Learning**: Datasets are split vertically based on the user feature dimension, and the part of the datasets that have similar users but differing user attributes is considered for training.

**Federated Transfer Learning**: Sample and feature spaces of two datasets differ, and transfer learning is utilized to overcome the absence of data or tags.

<img width="641" height="259" alt="image" src="https://github.com/user-attachments/assets/d217042f-2b0b-4932-a317-f5955bcc85c2" />

## Aggregation Algorithms

Adding or updating how exactly these decentralized clients will be connected to create a global model without sharing data is called aggregation algorithms.
- average aggregation
- clipped aggregation
- momentum aggregation
- bayesian aggregation
- secure aggregation
- quantization aggregation
- hierarchical aggregation
- 
## Aggregation algorithum and strategies 

- FedSGD
- FedSVRG
- FedAvg
- FedPer
- LG-FedAvg
- FedAws
- FedMA
- FedProx
- FedNova
- FedDist
- FedDyn

have to learn about these more depely rn i just read new names read some description about 2-3 line understand nothing hence i have to learn or atleast understand them to explain to anyone what the difference between each of these

## Federated Learning Framework

- TensorFlow
- PySyft
- Flower
- OpenFl
- PaddleFL
- FedML
- XayNet
- IBM federated learning
- Substra
- Nvidia Clara

## Challenges in Federated Learning

- **Privacy protection** - protecting sensitive user data from exposure
- **Communication cost** - high network overhead from frequent model updates
- **System heterogeneity** - diverse devices with varying computational capabilities
- **Unreliable model upload** - inconsistent client participation and connectivity

## Privacy-Preserving Federated Learning

### Need for Privacy Preservation

Federated learning, despite its decentralized training approach, faces several privacy vulnerabilities:

- **Gradient information leakage** - model updates can leak information about training data
- **Unreliable participants or clients** - malicious or compromised clients can poison the model
- **Honest but curious server** - the central server may attempt to infer private information from aggregated updates
- **Direct release of trained model** - the final model itself can memorize and expose training data

### Privacy-Enhancing Technologies

**1. Anonymization**

The technique for safeguarding data privacy by eliminating any personal information that could be used to identify a particular user. This prevents direct attribution of data to individuals.

**2. Differential Privacy (DP)**

By injecting noise or using a sample dataset, DP maintains statistical features and safeguards the privacy of data by preventing an attacker from getting exact information even after several searches. By introducing controlled noise, DP protects against computationally dominant adversaries.

DP is therefore not appropriate for small datasets and is best suited for large datasets. DP provides a notably higher level of protection with some degree of precision loss.

**3. Homomorphic Encryption (HE)**

A method that enables computation to be carried out on encrypted data without decrypting it. There are several techniques of encryption used for improving the model - as each type of encryption can allow specific types of operations on it to train models. Some have limitations like only a finite number of executions and finite number of operations can be performed.

**4. Secure Multi-Party Computation (SMPC)**

It permits several participants to collaboratively calculate a function on their confidential inputs without disclosing any details about their inputs to one another. Few techniques used are:

- Oblivious transfer
- Secret sharing
- Garbled circuits

### My Understanding: FL ≠ Automatic Privacy

Well, I thought FL means privacy, FL means data protection, FL means decentralized—but I guess I was wrong. FL means federated learning. It is better than normal ML models for privacy, but it alone is nothing. It requires different techniques, and the one I am targeting for my project can't be scaled easily because decentralized FL is still yet under research and not yet deployed or considered for deployment because of its limitations:

- **Scalability** - struggles to handle large numbers of participants efficiently
- **Adaptability** - difficult to adjust to dynamic network conditions
- **Heavy network burden** - decentralized coordination creates significant communication overhead

### A Real-World Example: The MoltBot/OpenClaw Problem

Well, I have got one doubt. A day before today I was reading about OpenClaw or MoltBot, and as I read, I understand it's still a project under development or progress. The builder made it open source and now anyone can help upgrade it and stuff. But in 2026, it is one of the biggest tech topics of discussion because of the problems it holds. Since the developer made anyone able to update the code and improve stuff, I think it is somewhat an example of centralized federated learning. Yes, the main power is still in the hands of the main developer, but anyone can contribute, download the model on their own laptop, improve it, make it learn stuff, and hence result in a better project at the end.

Do you think the example of MoltBot or OpenClaw is an example of why decentralized models—or even centralized ones—are still not scalable because of the flaws that apps like MoltBot now expose people to? It was good in research, but making it public for all made it harmful:

- **Not secure as needed to be** - open contribution without proper governance creates attack vectors
- **Lack of trust guarantees** - no mechanism to verify contributor intentions
- **Model poisoning risks** - malicious updates can compromise the entire system

## The Reality: FL Needs More Than Just Decentralization

Initially, federated learning was assumed to inherently provide strong privacy, security, and decentralization. However, deeper analysis shows that **FL is only a training paradigm and does not guarantee data protection on its own**. Fully decentralized FL systems are still largely research-oriented due to scalability, adaptability, network overhead, and security limitations. 

Public and open collaborative ML projects (e.g., MoltBot/OpenClaw) further highlight that **openness and decentralization can amplify misuse if governance and threat models are weak**. Thus, practical FL systems require additional mechanisms such as secure aggregation, differential privacy, and centralized coordination to be deployable and safe.

### Why Centralized FL?

- **Easier coordination** - single server orchestrates training rounds efficiently
- **Better quality control** - centralized entity can validate and filter model updates
- **Simpler security model** - clearer trust boundaries and threat model
- **Proven scalability** - existing infrastructure supports large-scale deployment
- **Faster convergence** - direct aggregation without peer-to-peer overhead

### Why Decentralized FL?

- **True privacy** - no single point of trust or failure
- **Resilience** - system continues even if some nodes fail
- **User autonomy** - participants have complete control over their data and participation
- **Censorship resistance** - no central authority can block participation
- **Aligned with FL philosophy** - truly distributed learning without centralized control


## Applications of Federated Learning

### Healthcare
- **Disease Prediction:** Enables hospitals to collaboratively train predictive models on patient data without sharing sensitive health records.
- **Medical Imaging Analysis:** Allows medical institutions to improve diagnostic accuracy by learning from distributed imaging datasets while maintaining patient privacy.

### Pharmaceutical Sector
- Facilitates drug discovery and clinical trial analysis across multiple research centers without centralizing proprietary or patient data.

### IoT
- **Real-time Anomaly Detection:** Enables edge devices to detect unusual patterns locally while collectively improving detection models across the network.

### Personalized Recommendation
- Powers recommendation systems that learn user preferences on-device, ensuring personalized experiences without uploading personal data to central servers.

### Autonomous Vehicles
- Allows vehicles to share learning from road experiences and edge cases while keeping location and usage data private on individual vehicles.

### NLP (Natural Language Processing)
- Enables keyboards and voice assistants to improve language models through on-device learning without transmitting users' typed or spoken content.

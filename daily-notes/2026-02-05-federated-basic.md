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
- quantization aggregation
- hierarchical aggregation

# Malware Detection Federal System

## Project Overview

So I am working on a project to create a malware detection model. Its speciality is that when training a model we generally use a centralized model that in case of malware can be both harmful for the device which we are sharing these documents with. Also, company-protected data might also get leaked because of this, which is not good.

## Our Solution

So my solution for this problem is to use a federated model that works on a local level. Instead of detecting breaches on a centralized server, we will detect the malware on your local computer and will share only the documentation to the centralized server. This will result in both privacy and data protection and helping in creating a rulebook from these documentations in creating a better, modified, and safe model for malware detection. This is our idea.

## Project Phases

So we have divided this project into 3 phases:

### Phase 1: Local Model Training
Using dataset and training model on local computer to give maximum accuracy and better model training. I will work specifically on maximizing its accuracy and F1 score. As soon as we finish with phase 1 model training on local host.

### Phase 2: Federated Learning Integration
We will start trying to add federated learning model and learn how to add the code in the model so that only documentation would be shared and every local computer will detect on its own only.

### Phase 3: Polishing Phase
In this phase we will build some custom clients and a rulebook that will get modified with these documentations. These clients will be running this model on local computer and sending info to centralized system or federal system. In the last, resulting in creating a better rulebook and securing privacy.

## Future Scope

In future scope, we will try to modify this specifically for IoT devices so that locally devices can protect themselves from malware.

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

# Phase 1: Model Development & Accuracy Optimization

well u have stated my idea pretty well but the real question comes now can i build it cause rn i worked upon maximising the accuracy and f1 score and stuff of my local model and for that the technique i am using is using multiple model that each work for improving the result i have used like 3 model each having their own purpose that provided me with the accuracy of around 95% but i realized when testing the model that it is deciding on the basis of pe files inside the document or .exe file like the advance file like explorer.exe or notepad.exe they now have huge role as they themselves are complex now and my model is declaring a file as malicious or being on the basis of whether it is using api-packages data transmission and stuff

## The Core Problem: False Positives

but i realized one main thing that these file in general do that and it doesnt make it like malicious so identifying a file to be malware now requires better or improved way cause rn my ai is marking anything malicious if it uses cpu usage at large level or uses api 

## Solution Attempt: Digital Signature Verification

so i decided to use signature digital certification of a file to be either verified by microsoft or google or any other approved signature that confirms that the file is fine and is not malicious but that too had downgrade cause in the case of stuxnet attack they just stole the signature from some company and used it in their malware and hence the first cyberwar globally recognised it was the result of poor malware detection rule so i decided not to use signature as just a if/else case i would setup a weightage to it 

## The Hybrid Approach: Signature Weightage + AI Behavior Analysis

like if a website have signature and it is verified than it lowers the chances of it being malicious by like 70% but still it can be malicious so here comes the role of my ai model 

it scans the file now and based upon it pe features or data inside it it gives it a value for malicious chances or % 

so in short having a signature makes u just clear one condition and not giving u a hall pass in my project tell now and then u still have to pass the ai behaviour check 

and if someone doesnt have this signature it will rated from 0-100% as it doesnt have signature it doesnt get the special privilege of getting around 70% off thing it have to be scanned for general case and given value

## Current Results & Performance

this is my idea and this resulted in decent 97.20% accuracy in a dataset of 50000 malware files and now it even detect computer local file by uploading it and scan and give them value 

for files like notepad.exe or explorer.exe before adding signature weightage thing it was giving these above two file as malicious and risky but now it is okay 

hence the project is working till now i gave u the whole technique i used for phase 1 local model training 

## Phase 1 Update: Technical Implementation & Optimization

### 🛠️ Strategic Feature Engineering (V7)
To address the limitations of standard behavioral analysis, I implemented a high-resolution feature extraction layer focusing on structural and statistical file nuances:

* **Adaptive Entropy Mapping:** Instead of a single entropy value, the model now analyzes **Byte Entropy Distributions**. This allows the AI to distinguish between "Natural Complexity" (seen in files like `explorer.exe`) and "Artificial Randomness" (typical of encrypted malware payloads).
* **API-Structural Correlation:** Introduced a relational feature that checks the ratio between **Import Address Table (IAT)** complexity and section entropy. This specifically targets "Packers" where malware hides its true API calls within compressed sections.
* **Byte-Density Histograms:** Integrated a 256-bin histogram analysis to capture the raw "fingerprint" of the binary, providing a deeper layer of identification beyond just file headers.

###  Weighted Reputation Logic
I transitioned from a binary "Trust/No Trust" system to a **Probabilistic Signature Anchor**:
* **Signature Weighting:** Verified digital certificates (Microsoft, Google, etc.) now provide a **70% safety influence**. 
* **Behavioral Override:** The remaining **30% risk assessment** is strictly controlled by the AI ensemble. This ensures that even "signed" files (addressing the Stuxnet-style stolen certificate vulnerability) must undergo a rigorous behavioral check before being cleared.

### 🚀 Performance & Accuracy Results
The integration of these custom features and the transition to a **Tuned Ensemble (LightGBM + XGBoost)** yielded significant improvements:

| Metric | Phase 1 Baseline | **Current Phase 1 (Tuned V7)** |
| :--- | :--- | :--- |
| **Model Accuracy** | 95.10% | **97.20%** |
| **F1-Score (Malware)** | 0.94 | **0.97** |
| **False Positive Rate** | High (System Files) | **Near Zero (System Files)** |

###  Real-World Predict Results
The model now demonstrates high stability on complex local binaries. 
* **`explorer.exe` & `notepad.exe`:** Previously flagged as high-risk, these are now correctly identified as **SAFE** with significantly lower risk scores (averaging **17% to 29%** AI risk) due to the reputation anchoring and entropy refinement.
* **Detection Confidence:** The AI "Confidence Distribution" shows a clearer separation between benign and malicious files, reducing the number of "Uncertain" cases.

---
**Next Step for Phase 2:** I will now initialize the Federated Learning environment by setting up the **Flower (flwr)** framework to enable decentralized training across multiple nodes.

## Future Scope

In future scope, we will try to modify this specifically for IoT devices so that locally devices can protect themselves from malware.

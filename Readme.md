# Network Intrusion Detection System (NIDS)

## 📌 Introduction
With the enormous growth of computer networks and applications, **network security** has become increasingly important.  
This project implements a **Network Intrusion Detection System (NIDS)** to detect anomalies and classify network attacks.

We tackle two problems:
1. **Binary Classification** – Normal vs Attack  
2. **Multiclass Classification** – Normal, DoS, Probe, R2L, U2R  

We improve attack classification by handling **class imbalance** with **SMOTE** and **VAE-based upsampling**, while keeping the **test set unchanged** for fair evaluation.

## 📂 Dataset
- Dataset: **KDDCUP99**
- Training samples: **144,767**
- Test samples: **28,954**
- Features: **42**
- Target Features:
  - `Attack` → (DoS, U2R, Probe, R2L)
  - `Is_Anomaly` → (1 = Attack, 0 = Normal)

### Class Distribution
**Train Set:**  
- DoS: 41,334  
- Normal: 61,643  
- Probe: 10,210  
- R2L: 2,555  
- U2R: 71  

**Test Set:**  
- DoS: 10,334  
- Normal: 15,411  
- Probe: 2,552  
- R2L: 639  
- U2R: 18  

---

## ⚙️ Approaches Implemented
### 1. Autoencoder + Neural Net
- Feature compression: 42 → 32
- Dual output heads:
  - Binary anomaly detection (Yes/No)
  - Attack type classification
- Upsampling with **SMOTE** and **VAE**
- Best results with VAE upsampling  
  **Hyperparameters (grid search):**
  - LR = 0.001  
  - Batch size = 512  
  - Dropout = 0.3  
  - Hidden sizes = (128, 64)

### 2. Transformer-based Approach
- Two-stage pipeline:
  1. **Anomaly Detector**
  2. **Attack Classifier**
- Components:
  - Dense layers + BatchNorm + Dropout
  - Multi-head Attention (Transformer Block)
- Results: ~**99% Accuracy** overall  
  (U2R performance lower due to rarity)

### 3. 1D CNN Approach
- 3-layer CNN with BatchNorm + ReLU
- Trained with CrossEntropy + Adam
- Captures **local feature dependencies**
- Results visualized with **Confusion Matrix**

---

## 📊 Results (Highlights)
- **VAE Autoencoder:** Best anomaly & attack classification
- **Transformer Model:** ~99% accuracy on binary anomaly detection
- **1D CNN:** Competitive performance, strong in DoS/Normal detection

---

## 📥 Installation
Clone the repo and install dependencies:
```bash
git clone https://github.com/Chiragkr28/COMPUTER-NETWORK-ANOMALY-DETECTION-.git
cd COMPUTER-NETWORK-ANOMALY-DETECTION-
pip install -r requirements.txt


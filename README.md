# 🚀 Large Hadron Collider Data Analysis  
---

## 📌 Overview  
This project was developed as part of the **Data Analytics track** at NSSC, IIT Kharagpur(2025)  
We worked on both **tabular** and **image-based datasets** to classify jet events into 5 categories and explored **anomaly detection** to identify rare or unknown physical phenomena.

---

## 📂 Dataset Summary  

- **Total Files(h5):** 27  
- **Entries per File:** 10,000  
- **Total Features:** 52  
- **Classes:** 5  

### Feature Types:
- **Kinematic Features**
- **Substructure Features**

---

## ⚙️ Data Preprocessing  

### Missing Data  
- No missing or sentinel values were found.  
- Hence, **no imputation** was required.

**Note:**  
If missing values were present, **median imputation** would be preferred due to:
- Robustness to outliers  
- Preservation of feature distribution  

⚠️ Improper imputation can distort **rare physics events**, leading to misclassification.

---

### Tabular Data Preparation  

#### Principal Component Analysis (PCA)  
- Reduced 52 features → **15 principal components**
- Covered ~**95% cumulative variance**

**Why PCA?**  
- Removes feature correlation  
- Reduces noise  
- Preserves dominant structure  

---

### 📊 Visualizations  
- Covariance Matrix  
- Explained Variance Ratio  
- Scree Plot  
- Distribution Plots (Count vs Feature)

---

## 🧠 Model Development  

---

### 📸 CNN on Image Data  

#### Architecture:
- **Conv2D Layers:**
  - 64 filters  
  - 128 filters  
  - 128 filters  
- **MaxPooling2D** after each layer  
- **Activation:** ReLU  

#### Fully Connected Layers:
- Flatten Layer  
- Dense Layers: 256, 128  
- Dropout: 0.3, 0.4  
- Output Layer:  
  - Units: 5  
  - Activation: Softmax  

#### ⚠️ Observations:
- Poor training performance due to:
  - Limited model capacity  
  - Small input size  
  - Non-optimal learning rate  

---

### 📊 Models on Tabular Data  

#### Model Choice: Random Forest Classifier  

**Why Random Forest?**
- Handles complex feature interactions  
- Resistant to overfitting (bagging + feature randomness)  
- Captures important features effectively  

---

## 📈 Performance Metrics  

| Metric     | Before PCA | After PCA |
|-----------|-----------|----------|
| Accuracy  | 0.825     | 0.798    |
| Precision | 0.827     | 0.800    |
| F1-Score  | 0.825     | 0.798    |
| ROC-AUC   | 0.963     | 0.951    |

---

## 🔍 Analysis  

- Increasing `n_estimators` led to **high computational cost with minimal gains**  
- PCA reduced dimensionality but slightly decreased accuracy  
- Likely reason:  
  → Low-variance features still hold **physical significance**  

### Key Issue:
- Difficulty distinguishing:
  - Class 0 (`b'j_g'`)
  - Class 1 (`b'j_q'`)

### Observations:
- Complex feature relationships  
- Possible lack of descriptive features  
- After PCA:
  - High overfitting OR poor accuracy depending on tuning  

---

## 🔄 Model Comparison  

| Aspect        | CNN (Image) | Random Forest (Tabular) |
|--------------|------------|--------------------------|
| Performance  | Lower      | Higher                  |
| Data Quality | Noisy (raw pixels) | Structured |
| Generalization | Poor (small dataset) | Better |

**Conclusion:**  
Tabular model performed better due to structured, meaningful features.

---

## 🚨 Anomaly Detection  

### Approach: Autoencoder  

#### Architecture:
- Encoder → Bottleneck → Decoder  
- Loss Function: **Mean Squared Error (MSE)**  

---

### 🔑 Bottleneck Size  
- Size: **64**  
- Ensures:
  - Strong compression  
  - Meaningful feature extraction  

---

### 📉 Training Result  
- Reconstruction Loss ≈ **4.6 × 10⁴**

---

### 📊 Threshold Selection  

- Error distribution: **Non-Gaussian**  
- Used **Percentile-Based Threshold**

| Percentile | Effect |
|-----------|-------|
| 90%       | High sensitivity, more false positives |
| 95%       | ✅ Optimal balance |
| 99%       | May miss rare events |

---

### 🔍 Interpretation of Anomalies  

Detected anomalies may correspond to:

- Rare **Standard Model processes**  
- **Beyond Standard Model (BSM)** phenomena  
- Exotic particle decays  
- Dark matter signatures  
- Instrumental noise  

---

## ⚠️ Limitations  

- Limited computational resources  
- Incomplete model comparison  
- CNN underperformance due to dataset size  
- PCA may discard physically relevant low-variance features  

---

## 🚀 Future Work  

- Explore advanced models:
  - Gradient Boosting (XGBoost, LightGBM)  
  - Hybrid CNN + Tabular models  
- Feature engineering based on physics insights  
- Improve anomaly detection with:
  - Variational Autoencoders (VAE)  
  - Isolation Forest  

---

## 👥 Team AstroSync  

- [Aayush Agarwal](https://github.com/AayushAgarwal-IITDelhi)  
- Aniruddha Ganbote
- [Vanshika Kataria](https://github.com/Vk2008)  

---
This project was submitted as part of **Impact Metrics, Jagriti 2026**.

---

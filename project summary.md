
---

# **SYN Flood Attack Detection Using Machine Learning**

---

## **1. Business Understanding**

SYN Flood attacks are a major cybersecurity threat, causing service outages, degraded performance, and financial losses.
Traditional Intrusion Detection Systems (IDS) often rely on static rules and signatures, which struggle to adapt to evolving attack strategies.

This project applies **Machine Learning (ML)** to build a scalable, robust, and interpretable IDS for detecting SYN Flood (DrDoS\_DNS) attacks in real-time network traffic.

---

## **2. Objectives**

1. **Build ML models** to classify network flows as benign or SYN Flood attack.
2. **Evaluate models** using multiple metrics: Accuracy, Precision, Recall, F1-score, ROC-AUC, Sensitivity, Specificity.
3. **Identify key traffic features** for better understanding of attack behavior and to guide IDS design.
4. **Deploy the best-performing model** for practical use in real-time systems.

---

## **3. Data Overview**

* **Dataset size:** 6703 network flows
* **Features:** 78 predictors including packet counts, flag counts (SYN, ACK, PSH, etc.), flow durations, rates, and packet length statistics
* **Label:** Binary (Benign = 0, DrDoS\_DNS = 1)
* **Class balance:** Almost balanced (Benign: 3034, Attack: 3669)
* **Missing values:** None – dataset is complete

---

## **4. Data Preparation**

* **Encoding:** Label encoded (Benign = 0, Attack = 1).
* **Correlation-based feature reduction:** Highly correlated features (|corr| > 0.95) dropped to avoid redundancy and overfitting.
* **Scaling:** StandardScaler applied to standardize numeric features.
* **Train-test split:** 70% training, 30% testing, stratified to maintain class balance.

---

## **5. Modeling & Evaluation**

### **Algorithms tested**

* **Ensemble:** Random Forest, Extra Trees
* **Boosting:** XGBoost, LightGBM, CatBoost
* **Kernel-based:** SVM (RBF kernel)
* **Distance-based:** K-Nearest Neighbors (optional tested variant)
* **ANN (Neural Net):** Simple feed-forward baseline

### **Performance Results**

* **ROC-AUC:** All models > 0.99
* **Best ROC-AUC:** 0.9998 (boosting/ensemble models)
* **Accuracy:** > 99% for all models
* **Sensitivity (Recall):** Up to **99.7%** → Very few attacks missed
* **Specificity:** Up to **99.7%** → Very few false alarms
* **Final model selection:** Based on ROC-AUC → Accuracy → Precision

📌 **Best model persisted for deployment**: `best_model.pkl`

---

## **6. Feature Importance (SHAP Analysis)**

### **Top 10 Features**

1. **Bwd PSH Flags**
2. **Fwd PSH Flags**
3. **Bwd Packets/s**
4. **Packet Length Max**
5. **Flow Packets/s**
6. **Flow Bytes/s**
7. **Fwd Packet Length Std**
8. **Fwd Packet Length Min**
9. **Protocol**
10. **Flow Duration**

📌 **Interpretation:**

* Flag counts and packet transmission rates are the most discriminative features.
* These directly reflect abnormal traffic bursts and incomplete handshakes typical of SYN Flood attacks.

---

## **7. Key Insights**

* **ML models detect SYN Flood attacks with near-perfect accuracy and recall.**
* **Packet/flag statistics and flow rates** are the most informative features.
* **Feature reduction** improved generalization and interpretability.
* **SHAP feature importance** provides actionable insights for designing IDS rules.

---

## **8. Business Impact**

* Enables **real-time ML-based IDS** with >99% detection accuracy.
* **Minimizes financial and service disruption risks** by drastically reducing undetected attacks.
* **Reduces false alarms**, improving trust in IDS alerts.
* Guides **network administrators** on monitoring critical features like packet rates and TCP flags for early detection.

---

## **Conclusion**

This project delivers a **robust, end-to-end ML pipeline** for SYN Flood detection:

* From **data exploration → feature engineering → modeling → evaluation → deployment**.
* Achieved **>99% accuracy, recall, and ROC-AUC**.
* Identified **key features** that explain model decisions and provide operational insights.

The approach is **generalizable to other network attacks** and can serve as a foundation for future **AI-driven security analytics**.

---


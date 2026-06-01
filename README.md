<p align="center">
  <img src="https://img.shields.io/badge/Python-3.12-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python"/>
  <img src="https://img.shields.io/badge/Scikit--Learn-1.8-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white" alt="Scikit-Learn"/>
  <img src="https://img.shields.io/badge/XGBoost-3.2-007EC6?style=for-the-badge&logo=xgboost&logoColor=white" alt="XGBoost"/>
  <img src="https://img.shields.io/badge/SHAP-0.52-FF6F00?style=for-the-badge" alt="SHAP"/>
  <img src="https://img.shields.io/badge/Streamlit-1.58-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white" alt="Streamlit"/>
</p>

<h1 align="center">🛡️ Explainable AI-Powered Fraud Detection System</h1>

<p align="center">
  <strong>A hybrid intelligent fraud detection system combining Anomaly Detection, Machine Learning Classification, and Explainable AI (XAI) for transparent, real-time financial transaction analysis.</strong>
</p>

<p align="center">
  <em>Developed by <strong>Deepak Kumar</strong></em>
</p>

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Key Features](#-key-features)
- [System Architecture](#-system-architecture)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Installation & Setup](#-installation--setup)
- [Usage](#-usage)
- [Model Performance](#-model-performance)
- [SHAP Explainability](#-shap-explainability)
- [Dashboard Preview](#-dashboard-preview)
- [How It Works](#-how-it-works)
- [Author](#-author)
- [License](#-license)

---

## 🔍 Overview

Financial fraud is a growing global threat, costing billions of dollars annually. Traditional rule-based systems fail to adapt to evolving fraud patterns. This project presents a **hybrid AI-powered fraud detection system** that not only detects fraudulent transactions with high accuracy but also **explains why** a transaction was flagged — making the AI decisions transparent and trustworthy.

The system employs a **three-stage pipeline**:

1. **Anomaly Detection** using Isolation Forest to identify unusual transaction patterns
2. **Classification** using Random Forest to classify transactions as fraudulent or legitimate
3. **Explainability** using SHAP (SHapley Additive exPlanations) to provide human-readable reasoning behind each prediction

---

## ✨ Key Features

| Feature | Description |
|---------|-------------|
| 🔬 **Hybrid Detection** | Combines unsupervised anomaly detection with supervised classification for robust fraud identification |
| 🧠 **Explainable AI (XAI)** | SHAP-based explanations provide transparent reasoning for every prediction |
| 📊 **Interactive Dashboard** | Beautiful Streamlit dashboard for real-time transaction analysis with visual insights |
| 📈 **K-Fold Cross Validation** | 5-fold stratified cross-validation ensures model reliability and generalization |
| 🎯 **High Accuracy** | Achieves ~98.5% precision and 100% recall across validation folds |
| ⚡ **Real-time Prediction** | Sub-100ms inference time for instant fraud detection |
| 📉 **Feature Importance** | Visual ranking of features contributing to fraud decisions |
| 🔄 **End-to-End Pipeline** | Complete ML pipeline from data preprocessing to model deployment |

---

## 🏗️ System Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                    FRAUD DETECTION PIPELINE                        │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│   ┌──────────────┐    ┌──────────────────┐    ┌──────────────────┐  │
│   │   Raw Data   │───▶│  Preprocessing   │───▶│ Feature Encoding │  │
│   │ (CSV Input)  │    │ (Scaling/Impute) │    │  (Label Encode)  │  │
│   └──────────────┘    └──────────────────┘    └────────┬─────────┘  │
│                                                         │           │
│                              ┌──────────────────────────┘           │
│                              ▼                                      │
│                  ┌─────────────────────┐                            │
│                  │  Isolation Forest   │                            │
│                  │ (Anomaly Detection) │                            │
│                  └──────────┬──────────┘                            │
│                             │ Anomaly Scores                        │
│                             ▼                                       │
│                  ┌─────────────────────┐                            │
│                  │  Random Forest      │                            │
│                  │  (Classification)   │                            │
│                  └──────────┬──────────┘                            │
│                             │ Predictions                           │
│                             ▼                                       │
│                  ┌─────────────────────┐                            │
│                  │   SHAP Explainer    │                            │
│                  │  (Explainability)   │                            │
│                  └──────────┬──────────┘                            │
│                             │                                       │
│                             ▼                                       │
│               ┌──────────────────────────┐                          │
│               │  Streamlit Dashboard     │                          │
│               │  (Interactive Results)   │                          │
│               └──────────────────────────┘                          │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

---

## 🛠️ Tech Stack

| Category | Technology |
|----------|-----------|
| **Language** | Python 3.12 |
| **ML Framework** | Scikit-Learn, XGBoost |
| **Explainability** | SHAP (TreeExplainer) |
| **Data Processing** | Pandas, NumPy |
| **Visualization** | Matplotlib, Plotly |
| **Web Dashboard** | Streamlit |
| **Model Serialization** | Joblib |

---

## 📁 Project Structure

```
explainable-fraud-detection/
│
├── 📂 data/
│   └── transactions.csv              # Transaction dataset (2500+ records)
│
├── 📂 models/
│   ├── fraud_classifier.pkl           # Trained Random Forest classifier
│   ├── isolation_forest.pkl           # Trained Isolation Forest model
│   ├── numeric_imputer.pkl            # Fitted numeric imputer
│   ├── numeric_scaler.pkl             # Fitted Standard Scaler
│   ├── TransactionType_encoder.pkl    # Label encoder - Transaction Type
│   ├── Location_encoder.pkl           # Label encoder - Location
│   ├── DeviceID_encoder.pkl           # Label encoder - Device ID
│   ├── IP Address_encoder.pkl         # Label encoder - IP Address
│   ├── MerchantID_encoder.pkl         # Label encoder - Merchant ID
│   ├── Channel_encoder.pkl            # Label encoder - Channel
│   └── CustomerOccupation_encoder.pkl # Label encoder - Occupation
│
├── 📂 outputs/
│   ├── shap_summary.png              # SHAP summary visualization
│   ├── shap_bar_plot.png             # Feature importance bar plot
│   ├── flagged_transactions.csv       # Flagged suspicious transactions
│   ├── augmented_dataset.csv          # Dataset with anomaly scores
│   ├── classification_results.csv     # Model classification outputs
│   ├── shap_values_per_transaction.csv # Per-transaction SHAP values
│   └── kfold_result_fold_*.csv        # K-Fold validation results
│
├── 📂 src/
│   ├── config.py                      # Configuration & hyperparameters
│   ├── preprocessing.py               # Data preprocessing pipeline
│   ├── anomaly.py                     # Isolation Forest anomaly detection
│   ├── classifier.py                  # Random Forest classifier training
│   ├── explainability.py              # SHAP explanation generation
│   └── dashboard_preprocessing.py     # Dashboard-specific preprocessing
│
├── main.py                            # Main training pipeline entry point
├── fraud_dashboard.py                 # Streamlit interactive dashboard
├── test_model.py                      # Model testing utilities
├── requirements.txt                   # Python dependencies
├── .gitignore                         # Git ignore rules
└── README.md                          # Project documentation
```

---

## 🚀 Installation & Setup

### Prerequisites

- Python 3.10 or higher
- pip (Python package manager)
- Git

### Step 1: Clone the Repository

```bash
git clone https://github.com/DEEPAK-317/explainable-fraud-detection.git
cd explainable-fraud-detection
```

### Step 2: Install Dependencies

```bash
pip install -r requirements.txt
pip install streamlit plotly tabulate
```

### Step 3: Run the Training Pipeline

```bash
python main.py
```

This will:
- Load and preprocess the transaction data
- Train the Isolation Forest anomaly detector
- Train the Random Forest classifier with 5-fold cross-validation
- Generate SHAP explanations and save visualizations

### Step 4: Launch the Dashboard

```bash
streamlit run fraud_dashboard.py
```

The dashboard will open at `http://localhost:8501`

---

## 📖 Usage

### Training Pipeline

```bash
python main.py
```

**Output:**
```
========== XAI Powered Fraud Detection Hybrid Pipeline ==========
[INFO] Loading dataset...
[INFO] Preprocessing dataset...
[INFO] Running Isolation Forest anomaly detection...
[INFO] Training classifier (RandomForest)...
[INFO] Generating SHAP explanations for classifier...
========== Hybrid Fraud Detection Pipeline Completed ==========
```

### Interactive Dashboard

```bash
streamlit run fraud_dashboard.py
```

Enter transaction details in the form and click **"Analyze Transaction"** to get:
- ✅ Fraud probability score
- 📊 SHAP feature impact visualization
- 🧠 Human-readable AI explanations
- ⚠️ Risk level assessment

---

## 📊 Model Performance

The model is evaluated using **5-Fold Stratified Cross-Validation**:

| Fold | Precision | Recall | F1 Score | ROC-AUC |
|------|-----------|--------|----------|---------|
| 1 | 1.0000 | 1.0000 | 1.0000 | 1.0000 |
| 2 | 1.0000 | 1.0000 | 1.0000 | 1.0000 |
| 3 | 1.0000 | 1.0000 | 1.0000 | 1.0000 |
| 4 | 0.9615 | 1.0000 | 0.9804 | 1.0000 |
| 5 | 0.9615 | 1.0000 | 0.9804 | 1.0000 |
| **Average** | **0.9846** | **1.0000** | **0.9922** | **1.0000** |

> 🎯 **Key Highlights:**
> - **98.46% Precision** — Very few false positives
> - **100% Recall** — Catches every fraudulent transaction
> - **99.22% F1 Score** — Excellent balance of precision and recall
> - **Perfect ROC-AUC** — Outstanding discrimination between classes

---

## 🧠 SHAP Explainability

The system uses **SHAP (SHapley Additive exPlanations)** to make AI decisions transparent and interpretable.

### Top Features by Impact

| Feature | Mean SHAP Value | Impact |
|---------|----------------|--------|
| AnomalyScore | 0.0699 | 🔴 Highest impact on fraud detection |
| LoginAttempts | 0.0148 | 🔴 Multiple login attempts increase fraud risk |
| TransactionType | 0.0073 | 🟡 Type of transaction influences prediction |
| TransactionDuration | 0.0050 | 🟡 Unusual durations flag suspicion |
| TransactionAmount | 0.0037 | 🟡 Amount anomalies raise alerts |
| AccountBalance | 0.0026 | 🟢 Balance context provides legitimacy signal |

### How SHAP Explanations Work

```
Transaction: $5,000 via Online channel
├── AnomalyScore: +0.069 (significantly increases fraud risk)
├── LoginAttempts: +0.015 (multiple attempts raise suspicion)
├── TransactionDuration: +0.005 (unusually fast transaction)
└── AccountBalance: -0.003 (healthy balance reduces risk)
    
Final Prediction: 🚨 FRAUD (87.3% probability)
Explanation: High anomaly score combined with multiple login 
attempts and rapid transaction speed indicate potential fraud.
```

---

## 🖥️ Dashboard Preview

The **Streamlit Dashboard** provides an intuitive interface for real-time fraud analysis:

### Features:
- 💳 **Transaction Input Form** — Enter transaction details (amount, type, location, channel, etc.)
- 📊 **SHAP Visualization** — Interactive bar chart showing feature contributions
- 🎯 **Risk Assessment** — Color-coded risk levels (Low / Medium / High)
- 🧠 **AI Explanations** — Human-readable reasoning for each prediction
- 📈 **Detailed Metrics** — Fraud probability, anomaly score, confidence level
- 🔬 **Advanced Analysis** — Expandable section with full feature contribution table

---

## ⚙️ How It Works

### Stage 1: Data Preprocessing
- **Date Parsing**: Converts transaction timestamps and calculates time differences
- **Numeric Scaling**: StandardScaler normalizes continuous features
- **Imputation**: Handles missing values using mean imputation
- **Label Encoding**: Converts categorical features (Location, Channel, etc.) to numeric

### Stage 2: Anomaly Detection (Isolation Forest)
- Identifies unusual transaction patterns without labeled data
- Uses `contamination=0.05` (5% expected anomaly rate)
- Generates **Anomaly Scores** that feed into the classifier as an additional feature

### Stage 3: Classification (Random Forest)
- 100-tree Random Forest ensemble trained on augmented features
- Uses Anomaly Score as an additional feature for improved accuracy
- Validated with 5-fold stratified cross-validation

### Stage 4: Explainability (SHAP)
- **TreeExplainer** computes exact Shapley values for tree-based models
- Generates per-feature impact scores for every prediction
- Produces human-readable explanations linking feature values to fraud risk

---

## 🔧 Configuration

Key parameters can be adjusted in `src/config.py`:

```python
RANDOM_STATE = 42          # Reproducibility seed
CONTAMINATION = 0.05       # Anomaly detection sensitivity (5%)
TEST_SIZE = 0.2            # Train/test split ratio
```

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

<p align="center">
  <strong>Developed with ❤️ by Deepak Kumar</strong>
</p>

<p align="center">
  <a href="https://github.com/DEEPAK-317">
    <img src="https://img.shields.io/badge/GitHub-DEEPAK--317-181717?style=for-the-badge&logo=github&logoColor=white" alt="GitHub"/>
  </a>
</p>
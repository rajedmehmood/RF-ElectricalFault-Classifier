# RF-ElectricalFault-Classifier

A structured study of **Random Forest classification** applied to electrical fault detection
and fault-type identification in simulated power grid systems. Built as direct preparation
for the **SmartNode-PK** Final Year Design Project — an Edge AI fault detection system for
low-voltage Pakistani power networks.

---

## Why This Exists

SmartNode-PK's edge layer deploys a **quantized Random Forest model on ESP32** to classify
electrical faults in real time. Before deploying any model on constrained hardware, you must
understand the algorithm deeply enough to defend every decision — feature selection, tree
depth, class imbalance handling, and quantization impact.

This repository documents that understanding, built from scratch on a real electrical
fault dataset.

---

## Dataset

**Source:** [Electrical Fault Detection and Classification — Kaggle](https://www.kaggle.com/datasets/esathyaprakash/electrical-fault-detection-and-classification/data)  
**Credit:** Esathya Prakash (2021)

The dataset simulates a power grid with four generators and multiple transmission lines.
Two CSV files are included:

| File | Task | Classes |
|---|---|---|
| `detect_dataset.csv` | Binary fault detection | Fault / No Fault |
| `classData.csv` | Multi-class fault classification | 6 fault types |

**Features:** Line currents (Ia, Ib, Ic) and voltages (Va, Vb, Vc) — three-phase
electrical measurements under various fault and normal conditions.

---

## Notebooks

### `fault_detection_binary.ipynb`
Binary classification — distinguishing a **faulted** system from a **healthy** one.

Covers:
- Exploratory Data Analysis (EDA) on three-phase current/voltage features
- Feature correlation and importance ranking
- Random Forest training and hyperparameter tuning
- Evaluation: accuracy, precision, recall, F1-score, confusion matrix

**Result:** `[fill in your accuracy]%` accuracy on test set

---

### `fault_classification_multiclass.ipynb`
Multi-class classification — identifying the **specific fault type** among 6 classes.

Covers:
- Class distribution analysis and imbalance handling
- Feature importance: which phase (current vs. voltage) matters most
- Random Forest with `n_estimators` tuning
- Multi-class confusion matrix and per-class F1 scores

**Result:** `[fill in your accuracy]%` accuracy on test set

---

## Key Technical Findings

> Fill this section after reviewing your notebooks — these are the findings that matter
> for SmartNode-PK.

- **Most predictive features:** `[e.g., Ia, Va showed highest feature importance]`
- **Minimum trees for stable accuracy:** `[e.g., n_estimators >= 100 showed diminishing returns]`
- **Hardest fault class to classify:** `[e.g., LG fault vs. LLG fault were most confused]`
- **Class imbalance impact:** `[note whether SMOTE or class_weight='balanced' was needed]`

---

## Setup

```bash
git clone https://github.com/rajedmehmood/RF-ElectricalFault-Classifier.git
cd RF-ElectricalFault-Classifier
pip install numpy pandas scikit-learn matplotlib seaborn jupyter
jupyter notebook
```

**Requirements:**
- Python 3.8+
- scikit-learn
- pandas
- matplotlib / seaborn

---

## Connection to SmartNode-PK

| This Repository | SmartNode-PK (FYDP) |
|---|---|
| RF on clean tabular data | RF quantized to INT8 on ESP32 |
| Three-phase current/voltage features | INA219 + ACS712 sensor telemetry |
| 6-class fault classification | Fault detection on LV Pakistani grid |
| sklearn implementation | Edge Impulse C++ deployment |

The feature importance rankings from this study directly inform **which sensors and
measurement windows** are worth implementing in SmartNode-PK's hardware design.

---

## Repository Structure

```
RF-ElectricalFault-Classifier/
│
├── fault_detection_binary.ipynb       # Binary: fault vs. no fault
├── fault_classification_multiclass.ipynb  # Multi-class: 6 fault types
├── detect_dataset.csv                 # Binary classification dataset
├── classData.csv                      # Multi-class classification dataset
└── README.md
```

---

## Author

**Rajed Mehmood**  
Electrical Engineering (Electronics), UET Lahore  
[linkedin.com/in/rajedmehmood](https://linkedin.com/in/rajedmehmood) |
[github.com/rajedmehmood](https://github.com/rajedmehmood)

*Part of the SmartNode-PK FYDP preparatory portfolio.*

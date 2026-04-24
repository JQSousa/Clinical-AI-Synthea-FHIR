# 🏥 Clinical AI with Synthea FHIR Data

> **Medication Recommendation System + Explainable AI for Clinical Decisions**  


---

## 🎯 Problem Statement

Two interconnected clinical AI challenges:

1. **Medication Recommendation** — Given a patient's clinical profile (conditions, demographics, lab values), suggest the most probable medications using multi-label classification and similarity-based systems.

2. **Explainable AI** — For every recommendation, generate a human-readable explanation: *"Why did the model predict high risk?"* — using SHAP values and feature attribution.

---

## 📊 Dataset

- **Source:** [Synthea™](https://synthetichealth.github.io/synthea/) — open-source synthetic patient generator
- **Interoperability:** FHIR R4 resource structure (Patient, Condition, MedicationRequest)
- **Size:** 800 patients, 14 conditions, 15 medications
- **Features:** Age, Sex, BMI, Systolic BP, HbA1c, eGFR, multi-label conditions

> ⚠️ All data is **synthetic** — no real patient information.

---

## 🧠 AI Approach

### Part 1 — Medication Recommendation

| Method | Description |
|---|---|
| **Multi-label Classification** | XGBoost + `MultiOutputClassifier` — one model per medication |
| **Similarity-based** | KNN over clinical feature space — "patients like this received..." |
| **Feature Engineering** | `MultiLabelBinarizer` on conditions, lab values, demographics |

**Why multi-label?** A patient can be on 5+ medications simultaneously. This mirrors real clinical complexity.

### Part 2 — Explainable AI (XAI)

| Tool | Role |
|---|---|
| **SHAP TreeExplainer** | Global feature importance + local patient-level attribution |
| **Waterfall plots** | Visual explanation for each prediction |
| **Clinical report** | Plain-language output: factors for/against recommendation |

**Why XAI in healthcare?** Regulatory frameworks (EU AI Act, FDA guidance) require explainability for AI-assisted clinical decisions. Black-box models are not acceptable.

---

## 🏗️ Architecture

```
Synthea FHIR Data
        │
        ▼
  Feature Engineering
  (MultiLabelBinarizer + LabelEncoder)
        │
        ├──► Multi-Label XGBoost ──► Medication Probabilities
        │
        ├──► KNN Similarity      ──► Similar Patient Profiles
        │
        └──► SHAP TreeExplainer  ──► Clinical Explanation Report
```

---

## 📁 Repository Structure

```
synthea-clinical-ai/
├── notebooks/
│   └── clinical_ai_synthea.ipynb     ← Main Colab notebook
├── docs/
│   └── clinical_explanation_report   ← Sample XAI output
├── README.md
└── requirements.txt
```

---

## 🚀 Run in Google Colab

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/)

```bash
# All dependencies
pip install shap scikit-learn xgboost pandas numpy matplotlib seaborn plotly
```

---

## 📈 Results

| Metric | Value |
|---|---|
| Mean ROC-AUC | ~0.91 |
| Hamming Loss | ~0.08 |
| Medications modelled | 15 |
| XAI method | SHAP TreeExplainer |

---

## 🔑 Results

- ✅ **FHIR-aware data structure** — mirrors real interoperability standards
- ✅ **Multi-label** — not naive single-output; reflects clinical reality  
- ✅ **Similarity systems** — analogous to Netflix-style collaborative filtering, applied to clinical profiles
- ✅ **Explainability first** — SHAP at global and local (per-patient) level
- ✅ **Clinical safety framing** — output always flagged as decision support, not replacement

---

## 🛠️ Technologies

`Python` · `XGBoost` · `scikit-learn` · `SHAP` · `Pandas` · `Matplotlib` · `Plotly` · `FHIR R4`

---

## 📚 References

- [Synthea Project](https://synthetichealth.github.io/synthea/)
- [FHIR R4 Specification](https://hl7.org/fhir/R4/)
- [SHAP Documentation](https://shap.readthedocs.io/)
- [EU AI Act — High-Risk AI Systems](https://artificialintelligenceact.eu/)


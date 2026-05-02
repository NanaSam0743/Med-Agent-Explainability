# X-Agent: Explainability Layer for Breast MRI Decision Support

## Overview
X-Agent extends MedAgent (Dabrowicki et al., 2025) by adding
three explainability novelties to a multimodal breast cancer
AI pipeline built on the MAMA-MIA dataset.

---

## Novel Contributions
- **GAP 1** — JSON Decision Trace Log (full pipeline auditability)
- **GAP 2** — RAG Clinical Citations (NCCN guideline grounding)
- **GAP 3** — Cross-Modal Conflict Detection (imaging vs pathology)


---

## Dataset
- **MAMA-MIA v2** — 225 patients
- DUKE (44) | ISPY2 (146) | ISPY1 (29) | NACT (6)
- Train: 155 | Val: 28 | Test: 42

---

## Pipeline Modules
| Module | Component | Type |
|--------|-----------|------|
| M1 | 3D U-Net Segmentation | Baseline |
| M2 | DenseNet121 Classification | Baseline |
| GAP 3 | Conflict Detection | Novel |
| M4 | BioBERT Text Encoding | Baseline |
| M5 | FiLM Fusion + pCR | Baseline + Novel |
| M6 + GAP 2 | LLM + RAG Citations | Novel |
| GAP 1 | JSON Decision Trace | Novel |

---

## Results

### Segmentation
| Metric | Ours | Paper |
|--------|------|-------|
| Dice (no augmentation) | 0.4728 | 0.8034 |
| Dice (with augmentation) | 0.4957 | 0.8034 |

### Classification
| Metric | Ours | Paper |
|--------|------|-------|
| Accuracy | 40.48% | 83.31% |
| AUC | 58.17% | 82.01% |
| F1 Score | 39.11% | 78.33% |

### Fusion
| Metric | Value |
|--------|-------|
| Subtype AUC | 100%  |
| pCR AUC | 71.4% |

### X-Agent Novelty Scorecard (42 test patients)
| Novelty | Result |
|---------|--------|
| Trace Completeness | 100% |
| Citation Coverage | 100% |
| Conflict Detection | 61.9% (26/42) |

---

## Setup

### Requirements
```bash
pip install monai transformers nibabel \
            scikit-image sentence-transformers \
            scikit-learn torch


Open notebook.ipynb in Google Colab
Mount Google Drive
Set dataset path to MAMA-MIA v2
Run cells in order (1 → 20)

---

## Why Gap Exists vs Paper
Factor              Ours        Paper
────────────────────────────────────
Training patients   155         1,054
Total patients      225         1,506
Augmentation        Yes         Unknown
GPU                 T4 (15GB)   Unknown


---

## Authors
- Harris Imran — 25I-7620
- Saqib Hussain — 25I-7634

**Department of Artificial Intelligence**
National University of Computer and Emerging Sciences
Islamabad, Pakistan | Session 2025-2027

---

## Reference
Dabrowicki, W., Rusiecki, A., Jelen, L. (2025).
Med-Agent: A Hybrid AI Agent for Multimodal Cancer Diagnosis.
Procedia Computer Science, 270, 3290-3299.```

### Run

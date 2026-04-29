# Med-Agent-Explainability
Agent-level explainability layer for breast DCE-MRI decision support.
# X-Agent: An Agent-Level Explainability Layer for Adaptive, Evidence-Grounded Breast MRI Decision Support

[![Python](https://img.shields.io/badge/Python-3.12-blue.svg)](https://www.python.org/)
[![Google Colab](https://img.shields.io/badge/Google%20Colab-F9AB00?logo=googlecolab&color=525252)](https://colab.research.google.com/)
[![Gemini API](https://img.shields.io/badge/Gemini%20API-Flash%20Lite-8A2BE2)](https://aistudio.google.com/)

**Institution:** National University of Computer and Emerging Sciences (FAST-NUCES), Islamabad, Pakistan  
**Program:** Master of Science in Artificial Intelligence (MSAI), Session 2025–2027  
**Authors:** Harris Imran & Saqib Hussain  

---

## 📌 Project Overview
Despite the high diagnostic accuracy of multimodal systems like Med-Agent, existing breast DCE-MRI pipelines often lack an agent-level explainability layer. They stop at module-level outputs (like masks or labels) and operate as a "black box," failing to document the end-to-end reasoning path.

**X-Agent** addresses this critical research gap. Built on top of the Med-Agent architecture and utilizing the MAMA-MIA dataset, X-Agent introduces a transparent decision trace, resolves cross-modal data conflicts, and grounds therapy advice in verifiable clinical evidence using Retrieval-Augmented Generation (RAG).

## ✨ Key Features
* **Cross-Modal Conflict Resolution:** Automatically detects discrepancies between MRI-derived imaging features and clinical pathology reports, resolving them through explicit logic (e.g., pathology overrides imaging).
* **Evidence Grounding (RAG):** Intercepts standard Large Language Model (LLM) prompts to inject verbatim citations from clinical guidelines (e.g., NCCN 2026), ensuring treatments are backed by established medical literature.
* **Agent-Level Traceability:** Generates a machine-readable JSON decision log (`x_agent_decision_log.json`) that captures inputs, conflict states, retrieved citations, and the final LLM rationale.

## ⚙️ Architecture Workflow
1.  **Phase 1–3 (Perception & Analysis):** 3D U-Net segmentation and DenseNet121 feature extraction (simulated via the MAMA-MIA benchmark).
2.  **Phase 4 (Consistency Check):** Cross-modal conflict detection between imaging and clinical variables.
3.  **Phase 5 (Decision & Report):** RAG escalation and output generation via the Google Gemini `2.5-flash-lite` model, producing both a clinician-facing narrative and an auditable trace.
 
### Usage Example
The core function simulates a multidisciplinary tumor board. You can pass patient parameters directly to test the conflict resolution and RAG layer:

```python
run_x_agent_tumor_board(
    age=48, 
    imaging_subtype="Luminal A", 
    clinical_subtype="HER2-enriched", 
    size=2.1, 
    volume=12.5, 
    pcr_prob=68.2
)

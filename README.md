# Multi-Modal Image Fusion for Enhanced Multi-Class Diagnosis of Cardiovascular Diseases Using Deep Learning

[![IEEE Xplore](https://img.shields.io/badge/IEEE%20Xplore-Published-00629B?style=for-the-badge&logo=ieee&logoColor=white)](https://ieeexplore.ieee.org)
[![Conference](https://img.shields.io/badge/C--CODE'25-4th%20International%20Conference-blue?style=for-the-badge)](https://ieeexplore.ieee.org)
[![Accuracy](https://img.shields.io/badge/Accuracy-99.75%25-brightgreen?style=for-the-badge)](https://ieeexplore.ieee.org)
[![Deep Learning](https://img.shields.io/badge/Deep%20Learning-ResNet50-orange?style=for-the-badge&logo=pytorch&logoColor=white)](https://ieeexplore.ieee.org)
[![XAI](https://img.shields.io/badge/XAI-Grad--CAM%20%7C%20SHAP-purple?style=for-the-badge)](https://ieeexplore.ieee.org)
[![ECG](https://img.shields.io/badge/ECG-Multi--Modal%20Fusion-red?style=for-the-badge)](https://ieeexplore.ieee.org)
[![HuggingFace](https://img.shields.io/badge/HuggingFace-CVD--ECG--AI-FFD21E?style=for-the-badge&logo=huggingface&logoColor=black)](https://huggingface.co/CVD-ECG-AI/ECG-CVD-ResNet50-MultiModal)

> Peer-reviewed research published in IEEE Xplore — applied deep learning for biomedical ECG diagnostics.

---

## Publication Details

| Field | Details |
|---|---|
| **Conference** | 4th International Conference on Communication, Computing and Digital Systems (C-CODE'25) |
| **Publisher** | IEEE Xplore |
| **Conference Date** | October 1–2, 2025 |
| **Venue** | Bahria University, Islamabad, Pakistan |
| **Published** | October 29, 2025 |
| **Peak Accuracy** | 99.75% |

**Authors:** Zain Abbas · Mohammad Haseeb · Hasan Mehdavi
**Supervisor:** Ms. Sania Urooj

---

## Abstract

Proposed a deep learning diagnostic framework that addresses the core limitation of single-modality ECG analysis. The pipeline transforms 1D ECG signals into four complementary 2D visual representations — Gramian Angular Fields (GAF), Markov Transition Fields (MTF), Recurrence Plots (RP), and Time-Frequency Representations (TFR) — which are fused and classified via a ResNet50 backbone. The resulting system achieves **99.75% classification accuracy** across five cardiovascular conditions, with Grad-CAM and SHAP providing full explainability for clinical deployment.

---

## Key Contributions

- **Novel ECG-to-image transformation pipeline:** 1D signals → GAF, MTF, Recurrence Plot, and TFR representations
- **Multi-class diagnosis** of Myocardial Infarction (MI), Coronary Artery Disease (CAD), Congestive Heart Failure (CHF), Arrhythmia (ARR), and Healthy Control (HC)
- **ResNet50 fusion backbone** achieving **99.75% classification accuracy** — among the highest reported for multi-class CVD detection in the literature
- **Explainable AI (XAI)** via Grad-CAM spatial saliency maps for per-class visual explanation
- **SHAP global attribution** for feature-level interpretability targeting physician trust and diagnostic transparency

---

## Pipeline Overview

```
Raw ECG Signal (1D)
        │
        ▼
┌─────────────────────────────────────────────────────┐
│              Stage 1 — Pre-Processing               │
│  Bandpass Filter → QRS Segmentation → Upsampling    │
└─────────────────────────────────────────────────────┘
        │
        ▼
┌─────────────────────────────────────────────────────┐
│           Stage 2 — Multi-Modal Image Generation    │
│                                                     │
│   GAF        MTF        RP         TFR              │
│  (128×128)  (128×128)  (128×128)  (128×128)         │
└─────────────────────────────────────────────────────┘
        │
        ▼
┌─────────────────────────────────────────────────────┐
│              Stage 3 — Image Fusion                 │
│      Pixel-wise average → Single fused image        │
└─────────────────────────────────────────────────────┘
        │
        ▼
┌─────────────────────────────────────────────────────┐
│          Stage 4 — Classification (ResNet50)        │
│   CAD · Healthy · MI · CHF · ARR   →  99.75% Acc   │
└─────────────────────────────────────────────────────┘
        │
        ▼
┌─────────────────────────────────────────────────────┐
│              Stage 5 — Explainability (XAI)         │
│            Grad-CAM  ·  SHAP Attribution            │
└─────────────────────────────────────────────────────┘
```

---

## Repository Structure

```
C-CODE-25-IEEE-Research/
│
├── notebooks/
│   ├── multiclass/                        # Multi-class classification experiments
│   │   ├── 5class_ARR_CHF_HC_MI_CAD.ipynb   ← Main paper model (5 classes, 99.75%)
│   │   ├── 4class_CHF_HC_MI_CAD.ipynb        ← Ablation: 4-class variant
│   │   └── 3class_HC_MI_CAD.ipynb            ← Ablation: 3-class variant
│   │
│   └── binary/                            # Binary classification baselines
│       ├── ARR_vs_HC.ipynb
│       ├── CAD_vs_HC.ipynb
│       ├── CHF_vs_HC.ipynb
│       └── MI_vs_HC.ipynb
│
├── models/                                # Trained model weights (*.h5 gitignored)
│   ├── multiclass/                        # See "Model Weights" section to download
│   │   ├── 5class_ARR_CHF_HC_MI_CAD_v1.h5
│   │   ├── 5class_ARR_CHF_HC_MI_CAD_v2.h5
│   │   └── 3class_HC_MI_CAD.h5
│   └── binary/
│       ├── CAD_vs_HC.h5
│       └── MI_vs_HC.h5
│
├── .gitignore
├── LICENSE
└── README.md
```

> **Note:** `.h5` model files and data files (`.csv`, images) are excluded from git tracking via `.gitignore`. See the [Model Weights](#model-weights) section below.

---

## Datasets

This work uses publicly available ECG databases:

| Dataset | Source | Classes Used |
|---|---|---|
| **PTB Diagnostic ECG** | [PhysioNet](https://physionet.org/content/ptbdb/1.0.0/) | MI, HC, CAD |
| **MIT-BIH Arrhythmia** | [PhysioNet](https://physionet.org/content/mitdb/1.0.0/) | ARR |
| **BIDMC CHF** | [PhysioNet](https://physionet.org/content/chf2db/1.0.0/) | CHF |

---

## Model Weights

Trained model weights are hosted on HuggingFace and are **not tracked in this git repository** (excluded via `.gitignore`).

**HuggingFace Repository:** [CVD-ECG-AI/ECG-CVD-ResNet50-MultiModal](https://huggingface.co/CVD-ECG-AI/ECG-CVD-ResNet50-MultiModal)

| Model File | Type | Description |
|---|---|---|
| `models/multiclass/5class_ARR_CHF_HC_MI_CAD_v1.h5` | Multi-class | Main paper model — 5 classes, **99.75% accuracy** |
| `models/multiclass/5class_ARR_CHF_HC_MI_CAD_v2.h5` | Multi-class | Alternative checkpoint |
| `models/multiclass/3class_HC_MI_CAD.h5` | Multi-class | 3-class ablation model |
| `models/binary/CAD_vs_HC.h5` | Binary | CAD vs Healthy Control |
| `models/binary/MI_vs_HC.h5` | Binary | MI vs Healthy Control |

### Download via Python

```python
from huggingface_hub import hf_hub_download

# Download the main 5-class model (99.75% accuracy)
model_path = hf_hub_download(
    repo_id="CVD-ECG-AI/ECG-CVD-ResNet50-MultiModal",
    filename="models/multiclass/5class_ARR_CHF_HC_MI_CAD_v1.h5"
)

# Load with Keras
from tensorflow import keras
model = keras.models.load_model(model_path)
```

### Download all models at once

```python
from huggingface_hub import snapshot_download

local_dir = snapshot_download(
    repo_id="CVD-ECG-AI/ECG-CVD-ResNet50-MultiModal",
    local_dir="./models"
)
print(f"Models saved to: {local_dir}")
```

---

## Requirements

All notebooks were developed and executed on **Google Colab** (Python 3.10, GPU runtime).

```bash
pip install wfdb PyWavelets mne pykalman
pip install numpy scipy matplotlib opencv-python
pip install tensorflow keras scikit-learn
pip install PyEMD==1.0.0 tensorflow-addons==0.22.0
pip install shap grad-cam seaborn tqdm
```

---

## Notebook Guide

| Notebook | Description | Classes | Best Accuracy |
|---|---|---|---|
| `5class_ARR_CHF_HC_MI_CAD.ipynb` | **Main paper model** — full 5-class pipeline with XAI | ARR, CHF, HC, MI, CAD | **99.75%** |
| `4class_CHF_HC_MI_CAD.ipynb` | 4-class ablation study | CHF, HC, MI, CAD | — |
| `3class_HC_MI_CAD.ipynb` | 3-class ablation study | HC, MI, CAD | — |
| `ARR_vs_HC.ipynb` | Binary: Arrhythmia vs Healthy | ARR, HC | — |
| `CAD_vs_HC.ipynb` | Binary: CAD vs Healthy | CAD, HC | — |
| `CHF_vs_HC.ipynb` | Binary: CHF vs Healthy | CHF, HC | — |
| `MI_vs_HC.ipynb` | Binary: MI vs Healthy | MI, HC | — |

Each multiclass notebook follows the same **5-stage pipeline**: pre-processing → image generation → fusion → ResNet50 training → XAI evaluation.

---

## Core Technologies

| Component | Technology |
|---|---|
| ECG Signal Processing | `wfdb`, `scipy.signal`, Pan-Tompkins QRS detection |
| Image Representations | GAF, MTF, Recurrence Plot, TFR (STFT-based) |
| Image Fusion | Pixel-wise averaging of 4 modal images |
| Classification Backbone | ResNet50 (ImageNet pre-trained, fine-tuned) |
| Explainability | Grad-CAM (spatial), SHAP (global attribution) |
| Training Environment | Google Colab, TensorFlow 2.x / Keras |

---

## Tags

![Deep Learning](https://img.shields.io/badge/-Deep%20Learning-FF6F00?style=flat-square)
![Biomedical AI](https://img.shields.io/badge/-Biomedical%20AI-E91E63?style=flat-square)
![ECG Analysis](https://img.shields.io/badge/-ECG%20Analysis-F44336?style=flat-square)
![Multi-Modal Fusion](https://img.shields.io/badge/-Multi--Modal%20Fusion-9C27B0?style=flat-square)
![ResNet50](https://img.shields.io/badge/-ResNet50-3F51B5?style=flat-square)
![XAI](https://img.shields.io/badge/-XAI-2196F3?style=flat-square)
![Grad-CAM](https://img.shields.io/badge/-Grad--CAM-03A9F4?style=flat-square)
![SHAP](https://img.shields.io/badge/-SHAP-00BCD4?style=flat-square)
![Cardiovascular Disease](https://img.shields.io/badge/-Cardiovascular%20Disease-009688?style=flat-square)
![Medical Imaging](https://img.shields.io/badge/-Medical%20Imaging-4CAF50?style=flat-square)
![Trustworthy AI](https://img.shields.io/badge/-Trustworthy%20AI-8BC34A?style=flat-square)

---

## Citation

If you use this work in your research, please cite:

```bibtex
@inproceedings{abbas2025multimodal,
  title     = {Multi-Modal Image Fusion for Enhanced Multi-Class Diagnosis of Cardiovascular Diseases Using Deep Learning},
  author    = {Zain Abbas, Sania Urooj Mohammad Haseeb,  Hasan Mehdavi},
  booktitle = {Proceedings of the 4th International Conference on Communication, Computing and Digital Systems (C-CODE'25)},
  year      = {2025},
  month     = {October},
  publisher = {IEEE},
  address   = {Bahria University, Islamabad, Pakistan}
}
```

---

## Read the Paper

[Read Full Paper on IEEE Xplore](https://ieeexplore.ieee.org)

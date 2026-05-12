# MTSK Article Classifier — LLM-Based Interpretable Classifier

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/)
[![Model: multilingual-e5-large](https://img.shields.io/badge/model-multilingual--e5--large-orange)](https://huggingface.co/intfloat/multilingual-e5-large)

Code and resources for the article:

> **An Interpretable LLM-Based Classifier for Research Articles on  
> Mathematics Teaching Specialized Knowledge (MTSK)**  


---

## Overview

This repository contains the full pipeline for fine-tuning and interpreting
a multilingual text classifier that assigns research articles to thematic
categories of the **Mathematics Teaching Specialized Knowledge (MTSK)** framework.

The model uses [`intfloat/multilingual-e5-large`](https://huggingface.co/intfloat/multilingual-e5-large)
as backbone, adds a dropout + linear classification head, and explains
predictions with **SHAP** token-level attributions.

---

## Thematic categories (labels)

| Label | Description |
|-------|-------------|
| T1    | Initial teacher training |
| T2    | Training of teacher educators |
| T3    | MTSK in different mathematical topics and levels |
| T4    | Development of MTSK |
| T5    | Extensions of the MTSK framework |

---

## Repository structure

```
mtsk-classifier/
├── notebooks/
│   └── Experimento_13_SEED7.ipynb   # Full experiment (Experiment 13, SEED=7)
├── outputs/                         # Figures generated during training
│   ├── training_curves.png
│   ├── confusion_matrix.png
│   └── shap_bar_T1–T5.png
├── docs/
│   └── data_availability.md         # Data availability statement (Taylor & Francis)
├── requirements.txt
├── LICENSE
└── README.md
```

---

## Results (Experiment 13 — SEED = 7)

| Metric          | Value  |
|-----------------|--------|
| Validation F1 (macro) | **0.7776** |
| Validation Accuracy   | **0.7966** |
| Base model      | multilingual-e5-large |
| Training epochs | up to 20 (early stopping, patience=3) |
| Optimizer       | AdamW, lr=5e-5 |
| Batch size      | 16 |
| Max length      | 128 tokens |

Three independent runs with fixed seeds (SEED = 3, 5, 7) were performed
to report mean ± standard deviation, as detailed in the paper.

---

## Reproducibility

All experiments use a fixed random seed for Python, NumPy, and PyTorch:

```python
SEED = 7
random.seed(SEED)
np.random.seed(SEED)
torch.manual_seed(SEED)
torch.cuda.manual_seed_all(SEED)
```

The notebook is self-contained and designed to run on **Google Colab (T4 GPU)**.

---

## Requirements

```
transformers>=4.40.0
datasets
torch>=2.0
peft
huggingface_hub
evaluate
scikit-learn
shap
matplotlib
seaborn
openpyxl
```

Install all dependencies:

```bash
pip install -r requirements.txt
```

---

## How to run

1. Upload your dataset file `DATACEROMTSK_AUMENTADO.xlsx` to Google Drive  
   under `MyDrive/TG Maestria/`.

2. Open `notebooks/MTSK_Classifier_Experimento13_SEED7.ipynb` in Google Colab.

3. Connect to a T4 or A100 GPU runtime.

4. Run all cells in order.

---

## Data availability

The dataset used in this study (293 annotated research articles on MTSK)
is described in `docs/data_availability.md`.  
Due to copyright restrictions on article abstracts, the dataset is available
upon reasonable request to the corresponding author.

---

## Fine-tuned model

The fine-tuned model weights are available on Hugging Face:

🤗 **[crojasce1/mtsk-classifier](https://huggingface.co/crojasc2/mtsk-classifier)**

## Citation

If you use this code or model in your research, please cite:

```bibtex
@misc{rojas2026mtsk,
  title         = {An Interpretable {LLM}-Based Classifier for Research Articles
                   on Mathematics Teaching Specialized Knowledge ({MTSK})},
  author        = {Rojas Celis, Carolina; Elorreaga, Luz Maricel and Hortúa Hector Javier},
  year          = {2026},
  note          = {Preprint. Manuscript submitted for publication.},
  howpublished  = {\url{https://github.com/crojasce1/mtsk-classifier}}
}
```

---


## License

This code is released under the **MIT License** — see [LICENSE](LICENSE).  
The base model `multilingual-e5-large` is released under MIT by Intfloat.

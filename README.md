# MTSK Article Classifier — LLM-Based Interpretable Classifier

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/)
[![Model: multilingual-e5-large](https://img.shields.io/badge/model-multilingual--e5--large-orange)](https://huggingface.co/intfloat/multilingual-e5-large)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.20148274.svg)](https://doi.org/10.5281/zenodo.20148274)

Code and resources for the article:

> **An Interpretable LLM-Based Classifier for Research Articles on Mathematics Teaching Specialized Knowledge (MTSK)**  
> Carolina Rojas Celis · Luz Maricel Elorreaga Rodríguez · Héctor Javier Hortúa  
> Universidad El Bosque — Maestría en Estadística Aplicada y Ciencia de Datos  
> *Manuscript submitted to Applied Artificial Intelligence*

---

## Overview

This repository contains two complementary analyses of the MTSK corpus (293 trilingual research articles in Spanish, English, and Portuguese):

1. **Supervised classifier** (`supervised/`) — Fine-tuned multilingual encoder (`intfloat/multilingual-e5-large`) with SHAP-based interpretability analysis.
2. **Unsupervised clustering** (`unsupervised/`) — Exploratory semantic analysis 
of the corpus using SBERT embeddings, UMAP (cosine metric), and HDBSCAN, 
designed to characterize the corpus's latent thematic structure independently 
of the supervised classification (ARI=0.047, NMI=0.111).
---

## Thematic categories (MTSK framework)

| Label | Description |
|-------|-------------|
| T1 | Applications of MTSK in teacher training |
| T2 | Research on mathematics teacher educators |
| T3 | MTSK in relation to different mathematical topics and levels |
| T4 | Theoretical development of the MTSK model |
| T5 | Extensions of the MTSK framework |

---

## Repository structure

```
mtsk-classifier/
├── unsupervised/
│   ├── mtsk_unsupervised_clustering.ipynb
│   ├── README.md
│   └── .gitignore
├── MTSK_Classifier_Experimento13_SEED7.ipynb
├── .gitignore
├── LICENSE
├── README.md
├── data_availability.md
├── guia_github_zenodo.md
└── requirements.txt
```

---

## Supervised Classifier — Key Results

| Metric | Value |
|--------|-------|
| F1-macro (test set, n=59) | **0.7776** |
| Accuracy | **0.7966** |
| Base model | intfloat/multilingual-e5-large |
| Training epochs | Up to 20 (early stopping, patience=3) |
| Optimizer | AdamW, lr=5×10⁻⁵ |
| Max token length | 128 |
| Fixed seed | SEED = 7 |

Performance by category:

| Category | Precision | Recall | F1 |
|----------|-----------|--------|----|
| T1 | 0.80 | 0.89 | 0.8421 |
| T2 | 0.90 | 1.00 | 0.9474 |
| T3 | 0.90 | 0.69 | 0.7826 |
| T4 | 0.75 | 0.82 | 0.7826 |
| T5 | 0.57 | 0.50 | 0.5333 |

---

## Unsupervised Clustering — Key Results

| Metric | Value |
|--------|-------|
| Groups discovered (HDBSCAN) | 7 |
| Outliers | 59 articles (20.1%) |
| ARI vs supervised T1–T5 | 0.047 |
| NMI vs supervised T1–T5 | 0.111 |

T1 and T2 show higher semantic cohesion. T3 and T5 
distribute diffusely across groups — consistent with 
SHAP interpretability findings in the supervised 
classifier. The low ARI confirms that T1–T5 categories 
encode expert theoretical criteria not visible in 
surface lexical signals.

See `unsupervised/README.md` for full details.


## Reproducibility

All experiments use fixed random seeds. The supervised notebook uses `SEED = 7`; the unsupervised notebook uses `SEED = 42`. Both notebooks are self-contained and designed to run on **Google Colab**.

Supervised requirements:
```
transformers>=4.40.0
torch>=2.0
scikit-learn
shap
datasets
```

Unsupervised requirements (pinned for reproducibility):
```
sentence-transformers==2.7.0
datasets==2.14.0
umap-learn
hdbscan
scikit-learn
```

Install all dependencies: `pip install -r requirements.txt`

---

## How to run

### Supervised classifier
1. Upload `DATACEROMTSK_AUMENTADO.xlsx` to Google Drive under `MyDrive/TG Maestria/`.
2. Open `MTSK_Classifier_Experimento13_SEED7.ipynb` in Google Colab.
3. Connect to a T4 or A100 GPU runtime.
4. Run all cells in order.

### Unsupervised clustering
1. Upload `DATACEROMTSK_AUMENTADO_SE.xlsx` to Google Drive under `MyDrive/TG Maestria/No supervisado/`.
2. Open `unsupervised/mtsk_unsupervised_clustering.ipynb` in Google Colab.
3. **Restart runtime after Cell 1** (library installation).
4. Run all cells in order.

---

## Data availability

The dataset (293 annotated research articles on MTSK) is described in [`data_availability.md`](data_availability.md). Due to copyright restrictions on article abstracts, the dataset is available upon reasonable request to the corresponding author.

The code and experimental notebooks are openly available on GitHub and archived on Zenodo:  
**DOI:** [10.5281/zenodo.20148274](https://doi.org/10.5281/zenodo.20148274)

---

## Citation

```bibtex
@misc{rojas2025mtsk,
  title        = {An Interpretable {LLM}-Based Classifier for Research Articles
                  on Mathematics Teaching Specialized Knowledge ({MTSK})},
  author       = {Rojas Celis, Carolina and Elorreaga Rodríguez, Luz Maricel
                  and Hortúa, Héctor Javier},
  year         = {2025},
  note         = {Manuscript submitted to Applied Artificial Intelligence},
  howpublished = {\url{https://github.com/crojasce1/mtsk-classifier}},
  doi          = {10.5281/zenodo.20148274}
}
```

---

## License

This code is released under the **MIT License** — see [LICENSE](LICENSE).  
The base model `multilingual-e5-large` is released under MIT by Intfloat.

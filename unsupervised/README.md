[README.md](https://github.com/user-attachments/files/27738849/README.md)

# Unsupervised Clustering Analysis — MTSK Corpus

Complementary analysis to:
**An Interpretable LLM-Based Classifier for Research Articles on
Mathematics Teaching Specialized Knowledge**

Carolina Rojas Celis · Luz Maricel Elorreaga Rodríguez · Héctor Javier Hortúa
Universidad El Bosque — Maestría en Estadística Aplicada y Ciencia de Datos

## Purpose

This folder contains an exploratory unsupervised clustering analysis of the
MTSK corpus (293 documents in Spanish, English, and Portuguese). The goal is
to characterize the latent thematic structure of the corpus independently of
the supervised classification.

**Note on model choice:** This analysis uses
`paraphrase-multilingual-MiniLM-L12-v2` for semantic embeddings — different
from the supervised classifier (`intfloat/multilingual-e5-large`). This is
intentional: the purpose is corpus characterization, not replication of the
classifier's internal representations.

## Pipeline

Corpus (293 docs)
→ Text preprocessing (title × 2 + abstract + keywords × 2)
→ SBERT embeddings (384d)  [paraphrase-multilingual-MiniLM-L12-v2]
→ L2 Normalization
→ UMAP 5D (metric=cosine, for clustering)
→ HDBSCAN (min_cluster_size=5, min_samples=5)
→ UMAP 2D (for visualization only, trained independently)
---
Note: PCA was deliberately excluded. A linear transformation would distort
the non-linear manifold structure preserved by UMAP with cosine metric.

## Files

| File | Description |
|------|-------------|
| `mtsk_unsupervised_clustering.ipynb` | Main notebook — run in Google Colab |
| `README.md` | This file |
| `.gitignore` | Excludes large binary files (.npy, .csv outputs) |

## Requirements
sentence-transformers==2.7.0
datasets==2.14.0
umap-learn
hdbscan
scikit-learn

```

Install via Cell 1 of the notebook (Google Colab).
Restart the runtime after Cell 1.

## Key Results

| Metric | Value |
|--------|-------|
| Groups discovered | 7 |
| Outliers | 59 articles (20.1%) |
| ARI (vs supervised T1–T5) | 0.047 |
| NMI (vs supervised T1–T5) | 0.111 |

The low ARI and NMI are expected and informative: the T1–T5 categories encode
expert theoretical criteria that do not emerge spontaneously from surface
lexical signals. T1 and T2 show higher semantic cohesion; T3 and T5 disperse
diffusely across groups, consistent with the interpretability findings in the
supervised classifier.

## Reproducibility

All random seeds are fixed (`random_state=42`).
Pre-computed embeddings can be saved via Cell 15 and reloaded to avoid
recalculation. Library versions are pinned in Cell 1.

## Related

- Supervised classifier: `/supervised` (or see root repository)
- Full paper: *Applied Artificial Intelligence* (under review)
- Data repository: see root `README.md`

[README.md](https://github.com/user-attachments/files/27738849/README.md)

# Unsupervised Clustering Analysis — MTSK Corpus

Complementary analysis to:  
**An Interpretable LLM-Based Classifier for Research Articles on Mathematics Teaching Specialized Knowledge**

Carolina Rojas Celis · Luz Maricel Elorreaga Rodríguez · Héctor Javier Hortúa  
Universidad El Bosque — Maestría en Estadística Aplicada y Ciencia de Datos

---

## Purpose

This folder contains an exploratory unsupervised clustering analysis of the MTSK corpus (293 documents in Spanish, English, and Portuguese). The goal is to characterize the **latent thematic structure of the corpus independently of the supervised classification** — not to validate the classifier's internal representations.

**Note on model choice:** This analysis uses `paraphrase-multilingual-MiniLM-L12-v2` for semantic embeddings. This differs deliberately from the supervised classifier (`intfloat/multilingual-e5-large`): since the purpose is corpus characterization rather than classifier analysis, a computationally efficient multilingual model is appropriate.

---

## Pipeline

```
Corpus (293 docs)
  → Text preprocessing (title × 2 + abstract + keywords × 2)
  → SBERT embeddings (384d)  [paraphrase-multilingual-MiniLM-L12-v2]
  → Normalization
  → PCA (384d → 50d, 85.5% variance retained)
  → UMAP 5D (for clustering)
  → KMeans / Hierarchical / GMM / DBSCAN
  → UMAP 2D (for visualization only)
```

---

## Files

| File | Description |
|------|-------------|
| `mtsk_unsupervised_clustering.ipynb` | Main notebook — run in Google Colab |
| `README.md` | This file |
| `.gitignore` | Excludes large binary files (.npy, .xlsx outputs) |

---

## Requirements

Pinned versions for reproducibility:

```
sentence-transformers==2.7.0
datasets==2.14.0
umap-learn==0.5.6
scikit-learn==1.3.2
```

Install via Cell 1 of the notebook (Google Colab). **Restart the runtime after Cell 1.**

---

## Key Results

| Configuration | Silhouette | Dominant themes per group |
|--------------|------------|--------------------------|
| K=3 (optimal) | 0.555 | G1→T4 (40.8%), G2→T1 (41.3%) |
| K=5 (reference) | 0.461 | G1→T4 (40.3%), G2→T1 (48.6%) |

- **T1 and T4** show stable semantic cohesion across both configurations.
- **T2, T3, T5** distribute diffusely — consistent with interpretability findings in the supervised classifier.
- DBSCAN identified **12 outlier articles** with peripheral or interdisciplinary content.
- ARI (K=3): 0.049 — low as expected; supervised labels encode expert theoretical criteria not visible in surface text.

---

## Reproducibility

All random seeds are fixed (`SEED = 42`). Pre-computed embeddings can be saved via Cell 14 and reloaded to avoid recalculation. Library versions are pinned in Cell 1.

---

## Related

- Supervised classifier: [`/supervised`](../supervised/) (or see root repository)
- Full paper: *Applied Artificial Intelligence* (under review)
- Data repository: see root `README.md`

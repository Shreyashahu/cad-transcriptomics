# Network-Guided Transcriptomic Feature Engineering for CAD Severity Classification

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Python 3.10](https://img.shields.io/badge/python-3.10-blue.svg)](https://www.python.org/)
[![bioRxiv](https://img.shields.io/badge/bioRxiv-preprint-red)](YOUR_BIORXIV_LINK_HERE)

**Authors:** Shreya Vinod Shahu, Jagdish Pimple  
**Affiliation:** Department of Information Technology, St. Vincent Pallotti College of Engineering and Technology, Nagpur, India  
**Preprint:** [bioRxiv — April 2026](YOUR_BIORXIV_LINK_HERE)

---

## Overview

This repository contains the complete reproducible analysis pipeline for the paper:

> *Network-Guided Transcriptomic Feature Engineering for Coronary Artery Disease
> Severity Classification: A Six-Stage Machine Learning Framework Using Whole-Blood RNA-seq*

We propose a six-stage pipeline that reduces 28,278 whole-blood RNA-seq genes to 55
biologically interpretable network features and achieves three-class CAD severity
classification (LOW / MID / CAD) with AUC = 0.86 / 0.79 / 0.69 using Random Forest.

---

## Key Results

| Model | CV F1 Macro | Test AUC (LOW) | Test AUC (MID) | Test AUC (CAD) |
|---|---|---|---|---|
| Random Forest (network-guided) | 0.461 | 0.86 | 0.79 | 0.69 |
| SVM (network-guided) | 0.465 | — | — | — |
| Random chance | 0.333 | 0.50 | 0.50 | 0.50 |

Top biomarker: **MRPS33** (mitochondrial ribosomal protein, importance = 0.043 ± 0.023)

---

## Data

RNA-seq data are publicly available from NCBI GEO:

- **Accession:** [GSE221911](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE221911)
- **Original study:** McCaffrey et al., 2023, *J. Mol. Cell. Cardiol. Plus*
- **Cohort:** 177 patients undergoing coronary catheterisation (after preprocessing: n = 168)

Raw data are not stored in this repository. Download instructions are in `data/README.md`.

---

## Reproducing the Analysis

### 1. Clone and set up environment

```bash
git clone https://github.com/Shreyashahu/cad-transcriptomics.git
cd cad-transcriptomics
conda env create -f environment.yml
conda activate cad-transcriptomics
```

### 2. Download data

Follow instructions in `data/README.md` to download GSE221911 from GEO and place
files in `data/processed/`.

### 3. Run notebooks in order

```bash
jupyter notebook notebooks/01_preprocessing.ipynb
```

Run notebooks 01 through 06 sequentially. Each notebook saves intermediate outputs
to `results/` that are loaded by the next notebook.

### 4. Run all at once (optional)

```bash
jupyter nbconvert --to notebook --execute notebooks/*.ipynb
```

---

## Pipeline Summary

| Stage | Script/Notebook | Description |
|---|---|---|
| 1. Preprocessing | `01_preprocessing.ipynb` | Filtering, CPM normalization, ComBat, outlier removal |
| 2. DEA | `02_DEA_and_clustering.ipynb` | ANOVA, top 1,000 DEGs |
| 3. Network features | `02_DEA_and_clustering.ipynb` | K-Means co-expression, eigengenes, hub genes |
| 4. ML classification | `03_ML_classification.ipynb` | 5 classifiers, GridSearchCV, LOOCV |
| 5. Feature importance | `04_feature_importance.ipynb` | Permutation importance, 30 repetitions |
| 6. Pathway enrichment | `05_pathway_enrichment.ipynb` | KEGG + GO via Enrichr API |

---

## Requirements

See `requirements.txt`. Key dependencies:

- Python 3.10
- scikit-learn 1.4.2
- pandas, numpy, scipy
- pydeseq2 / combat-seq (batch correction)
- gseapy (pathway enrichment)
- matplotlib, seaborn

---

## Citation

If you use this code or data, please cite:

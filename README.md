# Network-Guided Transcriptomic Feature Engineering for Coronary Artery Disease Severity Classification

A six-stage machine learning framework using whole-blood RNA-seq data for
three-class CAD severity classification.

**Authors:**  
- Shreya Shahu — St. Vincent Pallotti College of Engineering and Technology, Nagpur, India  
- Ashwini Shahu — City Premier College, Nagpur, India  
- Srushti Shahu — G H Raisoni College, Nagpur, India  
- Jagdish Pimple — St. Vincent Pallotti College of Engineering and Technology, Nagpur, India

**Status:** Preprint submitted to Elsevier

---

## Overview

Coronary Artery Disease (CAD) is the leading cause of death worldwide.
This study proposes a six-stage network-guided transcriptomic feature
engineering framework for non-invasive three-class CAD severity
classification using whole-blood RNA sequencing data.

**Key findings:**
- Network-guided co-expression features outperform naive gene selection by 26–28% in F1 macro score
- Random Forest achieved AUC values of 0.86, 0.79, and 0.69 for LOW, MID, and CAD severity classes
- MRPS33 is the most consistent and reproducible blood transcriptomic biomarker for CAD severity
- Progressive downregulation of ribosomal machinery is identified as a molecular hallmark of CAD severity

---

## Repository Structure

```
cad-transcriptomics/
│
├── README.md
├── requirements.txt
├── .gitignore
│
├── data/
│   └── README.md
│
├── notebooks/
│   └── CAD_Project.ipynb
│
├── figures/
│   ├── fig1_pipeline.png
│   ├── fig2a_pca.png
│   ├── fig2b_heatmap.png
│   ├── fig3_feature_comparison.png
│   ├── fig4_roc.png
│   ├── fig5_importance.png
│   └── fig6_pathway.png
│
└── paper/
    ├── cas-dc-template.tex
    └── cas-refs.bib
```

---

## Data

The dataset used in this study is publicly available from the
**Gene Expression Omnibus (GEO)** repository:

- **Accession:** GSE221911
- **Link:** https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE221911
- **File:** `GSE221911_Illumina_raw_read_count_177_pt.xlsx`

Download the file and place it in the `data/` folder before running
the notebook.

> The raw data file is not included in this repository due to its size.

---

## Pipeline Overview

The six-stage pipeline consists of:

1. **Preprocessing** — Gene filtering, CPM normalization, ComBat batch correction, sex-linked gene removal
2. **Exploratory Data Analysis** — PCA-based outlier removal, hierarchical clustering, quality validation
3. **Differential Expression Analysis** — One-way ANOVA, Benjamini-Hochberg FDR correction, top 1,000 DEG selection
4. **Co-expression Network Construction** — K-Means clustering, silhouette coefficient optimization, module-trait association
5. **Feature Matrix Construction** — Module eigengenes, hub gene identification, 99.8% dimensionality reduction (28,278 → 55 features)
6. **Machine Learning & Validation** — Five classifiers, stratified 5-fold CV, LOOCV, permutation feature importance, pathway enrichment analysis

---

## Requirements

Python 3.10 is required. Install all dependencies using:

```bash
pip install -r requirements.txt
```

---

## How to Run

1. Clone the repository:

```bash
git clone https://github.com/Shreyashahu/cad-transcriptomics.git
cd cad-transcriptomics
```

2. Install dependencies:

```bash
pip install -r requirements.txt
```

3. Download the dataset from GEO (GSE221911) and place it in `data/`

4. Open and run the notebook:

```bash
jupyter notebook notebooks/CAD_Project.ipynb
```

Run all cells from top to bottom. The notebook is self-contained and
will reproduce all results, tables, and figures from the paper.

---

## Results Summary

| Feature Set | F1 Macro | Accuracy |
|---|---|---|
| Network-guided (55 features) | 0.418 | 0.446 |
| Top 55 raw genes | 0.310 | 0.360 |
| Top 55 DE genes | 0.302 | 0.349 |
| All 1,000 DE genes | 0.468 | 0.491 |
| Random chance | 0.333 | 0.333 |

| Class | AUC (OvR) |
|---|---|
| LOW | 0.86 |
| MID | 0.79 |
| CAD | 0.69 |

---

## Citation

If you use this code or find this work useful, please cite:

```
Shahu, S., Shahu, A., Shahu, S., & Pimple, J. (2025).
Network-Guided Transcriptomic Feature Engineering for Coronary Artery
Disease Severity Classification: A Six-Stage Machine Learning Framework
Using Whole-Blood RNA-seq. Preprint submitted to Elsevier.
```

---

## Acknowledgements

The authors thank Timothy A. McCaffrey and colleagues at The George
Washington University for making the TruCAD RNA-seq dataset (GSE221911)
publicly available on the Gene Expression Omnibus repository.

---

## License

This project is licensed under the MIT License.  
See the [LICENSE](LICENSE) file for details.

---

## Contact

- **Shreya Shahu** — shreyashahu1404@gmail.com
````

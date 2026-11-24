# Network-Guided Transcriptomic Feature Engineering for Coronary Artery Disease Severity Classification

A six-stage machine learning framework using whole-blood RNA-seq data for three-class CAD severity classification.

**Authors:**
- Shreya Shahu — St. Vincent Pallotti College of Engineering and Technology, Nagpur, India
- Ashwini Shahu — City Premier College, Nagpur, India
- Srushti Shahu — G H Raisoni College, Nagpur, India
- Jagdish Pimple — St. Vincent Pallotti College of Engineering and Technology, Nagpur, India

**Status:** Under review, STAR Global Conference (2026)

## Overview

Coronary Artery Disease (CAD) is the leading cause of death worldwide. This project builds a network-guided transcriptomic feature engineering pipeline for non-invasive, three-class CAD severity classification (LOW / MID / CAD) from whole-blood RNA sequencing data.

**Key findings**

- The pipeline reduces 28,278 genes to 55 features (99.8% reduction) using K-Means co-expression clustering, module eigengene extraction, and hub gene identification.
- Network-guided features outperform feature sets of the same size built from top raw genes or top differentially expressed genes. A model using all 1,000 DE genes scores higher, so the contribution of this approach is compactness and interpretability, not peak accuracy.
- The best model (Random Forest) reached one-vs-rest AUCs of 0.69–0.86 across severity classes under leave-one-out cross-validation (168 samples), after target leakage was detected and corrected.
- MRPS33 is the top candidate biomarker, and KEGG Ribosome pathway enrichment is significant (p < 0.0001), consistent with progressive downregulation of ribosomal machinery with CAD severity.
- Results come from a single public cohort. External validation has not yet been completed, so the biomarker findings should be read as candidates.

## Repository Structure

```
cad-transcriptomics/
├── README.md
├── requirements.txt
├── .gitignore
├── LICENSE
├── data/
│   └── README.md
├── notebooks/
│   └── CAD_Project.ipynb
└── figures/
    ├── fig1_pipeline.png
    ├── fig2a_pca.png
    ├── fig2b_heatmap.png
    ├── fig3_feature_comparison.png
    ├── fig4_roc.png
    ├── fig5_importance.png
    └── fig6_pathway.png
```

## Data

The dataset is publicly available from the Gene Expression Omnibus (GEO):

- **Accession:** GSE221911
- **Link:** https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE221911
- **File:** `GSE221911_Illumina_raw_read_count_177_pt.xlsx`

Download the file and place it in `data/` before running the notebook. The raw file is not included in this repository due to its size.

## Pipeline

1. **Preprocessing** — gene filtering, CPM normalization, ComBat batch correction, sex-linked gene removal
2. **Exploratory data analysis** — PCA-based outlier removal, hierarchical clustering, quality validation
3. **Differential expression** — one-way ANOVA, Benjamini-Hochberg FDR correction, top 1,000 DEG selection
4. **Co-expression network construction** — K-Means clustering, silhouette optimization, module-trait association
5. **Feature matrix construction** — module eigengenes and hub gene identification (28,278 → 55 features)
6. **Machine learning and validation** — five classifiers tuned over 180 hyperparameter combinations, LOOCV (168 samples), permutation feature importance, pathway enrichment (Enrichr, KEGG)

### Leakage control

An earlier version of the pipeline leaked target information into the feature construction step. This was detected and corrected, and all reported results come from the corrected pipeline.

## Results

> **TODO before publishing:** the numbers below come from the earlier README. Re-run the corrected notebook and confirm each value, including the sample count, before this goes public.

| Feature set | F1 macro | Accuracy |
|---|---|---|
| Network-guided (55 features) | 0.418 | 0.446 |
| Top 55 raw genes | 0.310 | 0.360 |
| Top 55 DE genes | 0.302 | 0.349 |
| All 1,000 DE genes | 0.468 | 0.491 |
| Random chance | 0.333 | 0.333 |

| Class | AUC (one-vs-rest) |
|---|---|
| LOW | 0.86 |
| MID | 0.79 |
| CAD | 0.69 |

## Limitations

- Single cohort with a modest sample size; no external validation yet.
- Absolute performance on the CAD class is modest (AUC 0.69).
- The 55-feature set does not beat the full 1,000-gene DE set on F1 or accuracy.

## Requirements and How to Run

Python 3.10 is required.

```bash
git clone https://github.com/Shreyashahu/cad-transcriptomics.git
cd cad-transcriptomics
pip install -r requirements.txt
jupyter notebook notebooks/CAD_Project.ipynb
```

Download the GEO dataset into `data/` first, then run all cells from top to bottom.

## Citation

If you use this code, please cite:

Shahu, S., Shahu, A., Shahu, S., & Pimple, J. (2026). *Network-Guided Blood Transcriptomics for CAD Severity Classification: A Six-Stage Machine Learning Framework Using Whole-Blood RNA-seq.* Under review, STAR Global Conference.

## Acknowledgements

The authors thank Timothy A. McCaffrey and colleagues at The George Washington University for making the TruCAD RNA-seq dataset (GSE221911) publicly available.

## License

MIT License. See `LICENSE` for details.

## Contact

Shreya Shahu — shreyashahu1404@gmail.com · [LinkedIn](https://linkedin.com/in/shreyashahu)

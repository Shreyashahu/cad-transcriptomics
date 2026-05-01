# Data

The raw data used in this study is **not included** in this repository
due to file size constraints.

## Download Instructions

1. Go to the GEO repository:  
   https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE221911

2. Download the file:  
   `GSE221911_Illumina_raw_read_count_177_pt.xlsx`

3. Place the downloaded file in this `data/` folder:
   ```
   cad-transcriptomics/
   └── data/
       └── GSE221911_Illumina_raw_read_count_177_pt.xlsx
   ```

4. The notebook will automatically read the file from this location.

## About the Dataset

| Field | Details |
|---|---|
| **Accession** | GSE221911 |
| **Study** | TruCAD |
| **Patients** | 177 |
| **After QC** | 168 |
| **Sequencing** | Illumina total RNA-seq (rRNA-depleted) |
| **Batches** | TR1 (n = 82), TR2 (n = 95) |
| **Classes** | LOW (n = 73), MID (n = 42), CAD (n = 53) |

## Class Definitions

| Class | Stenosis | Description |
|---|---|---|
| LOW | < 50% | No significant or minimal disease |
| MID | 50–99% | Intermediate disease severity |
| CAD | ≥ 100% | Confirmed coronary artery disease |

## Original Study

McCaffrey, T.A., et al. (2023). RNAseq profiling of blood from patients
with coronary artery disease: Signature of a T cell imbalance.
*Journal of Molecular and Cellular Cardiology Plus*, 4, 100033.

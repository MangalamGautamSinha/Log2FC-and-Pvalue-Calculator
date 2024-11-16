# Log2 Fold Change and P-Value Calculator

This repository contains a Python script to calculate the log2 fold change (log2FC) and p-values for gene expression data. The script compares average FPKM (Fragments Per Kilobase of transcript per Million mapped reads) values between tumor and normal samples to identify gene expression differences.

## Features
- Calculates the average FPKM for each gene across tumor and normal samples.
- Computes fold change (FC) as the ratio of average FPKM in tumor to normal samples.
- Computes log2FC to quantify differential expression.
- Assigns regulation status:
  - `Up`: log2FC > 2
  - `Down`: log2FC < -2
  - `-`: Otherwise
- Performs a t-test to calculate p-values for statistical significance.
- Saves results as a CSV file.

## Getting Started

### Prerequisites
Ensure the following are installed:
- Python 3.8 or above
- Required Python libraries:
  - `pandas`
  - `numpy`
  - `scipy`

Install the libraries using:
```bash
pip install pandas numpy scipy
```

### Input Files
1. **Tumor File**: `m_merged.csv`
   - Contains merged FPKM data for tumor samples.
2. **Normal File**: `normal_merged.csv`
   - Contains merged FPKM data for normal samples.

Both files should:
- Have a `gene_id` and `gene_name` column.
- Include FPKM values for each sample in subsequent columns.

### Output File
- The script saves results to `./Log2FC_Avg_pvalue/m_vs_normal_Log2FC_pvalue.csv`.

### Usage
1. Place the tumor and normal merged files (`m_merged.csv` and `normal_merged.csv`) in the working directory.
2. Run the script in a Python environment:
   ```bash
   python script_name.py
   ```
3. The output file will contain:
   - `gene_id` and `gene_name`
   - Average FPKM for normal and tumor samples
   - Fold change (`FC`)
   - Log2 fold change (`log2FC`)
   - Regulation status
   - p-value for statistical significance

### Example Output

| gene_id        | gene_name  | Avg_FPKM_normal | Avg_FPKM_tumor | FC   | log2FC | Regulation | pvalue   |
|----------------|------------|-----------------|----------------|------|--------|------------|----------|
| ENSG000001     | GeneA      | 12.3            | 24.6           | 2.0  | 1.0    | -          | 0.03     |
| ENSG000002     | GeneB      | 3.5             | 0.5            | 0.14 | -3.0   | Down       | 0.01     |

## Notes
- Fold change (`FC`) values with `inf` or `NaN` are handled appropriately.
- A regulation threshold of ±2 log2FC is used for categorizing up/down regulation.
- Statistical p-values are computed using a two-sample t-test assuming equal variance.

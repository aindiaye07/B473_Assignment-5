# B473_Assignment-5

# Differential Gene Expression & Exploratory Data Analysis in R

## 1. Project & Author Information
* **Author:** Aissatou Ndiaye
* **Course:** INFO-B 473 – Application Programming for Biomedical Data Analysis
* **Date:** November 23, 2026
* **Language & Environment:** R (version 4.3.0 or higher)
* **Purpose:** This program loads multi-format biomedical datasets (`.xlsx`, `.csv`, `.tsv`), maps sample phenotypes to gene expression profiles, calculates group-level mean expression and $\log_2$ fold changes between Tumor and Normal tissues, filters for significantly differentially expressed genes ($|\log_2\text{FC}| > 5$), and generates exploratory data visualizations.

---

## 2. Required Input Files
Before running the script, place the following three input files in the **same working directory** as the R script (`gene_expression_analysis.R`):
1. **`Gene_Expression_Data.xlsx`** – Excel spreadsheet containing raw gene expression values with probes in rows and sample IDs in columns.
2. **`Gene_Information.csv`** – Comma-separated annotation file mapping Probe IDs to gene metadata and chromosomal locations.
3. **`Sample_Information.tsv`** – Tab-separated metadata file linking Sample IDs to their clinical phenotype (`Tumor` or `Normal`).

---

## 3. Dependencies & Required R Packages
This script uses Base R alongside the following CRAN libraries:
* **`readxl`**: Reads `.xlsx` spreadsheet files into R data frames.
* **`dplyr`**: Handles data frame filtering, column selection, mutations, and table joins.
* **`ggplot2`**: Generates histograms/bar charts of DEG chromosomal distributions and regulation percentages.
* **`pheatmap`**: Generates sample-by-gene expression heatmaps and hierarchical clustermaps.

To install all required libraries prior to running the script, execute the following command in your R console:
```r
install.packages(c("readxl", "dplyr", "ggplot2", "pheatmap"), repos = "https://r-project.org")
```

---

## 4. How to Run the Script on Any Machine
1. **Download Files:** Save `gene_expression_analysis.R` and the three input files (`Gene_Expression_Data.xlsx`, `Gene_Information.csv`, and `Sample_Information.tsv`) into a single folder.
2. **Set Working Directory:** Open R or RStudio and set your working directory to the folder containing your files:
   ```r
   setwd("path/to/your/folder")
   ```
3. **Install Packages:** Run the `install.packages(...)` command from Section 3 if the libraries are not already installed on your machine.
4. **Execute the Program:**
   * **From R or RStudio:**
     ```r
     source("gene_expression_analysis.R")
     ```
   * **From a Terminal / Command Prompt:**
     ```bash
     Rscript gene_expression_analysis.R
     ```

---

## 5. Program Workflow & Expected Outputs
### Analysis Steps Performed
1. Loads expression, gene annotation, and sample metadata files into R.
2. Renames sample columns in the expression dataset to reflect their phenotype (`Tumor` or `Normal`) from `Sample_Information.tsv`.
3. Splits the dataset into separate Tumor and Normal subsets and computes average expression per probe across each group.
4. Computes $\log_2$ fold change between Tumor and Normal groups and merges results with `Gene_Information.csv`.
5. Filters for probes with $|\log_2\text{FC}| > 5$ and labels each gene according to whether expression is higher in `Tumor` or `Normal` samples.
6. Generates exploratory visualizations examining chromosomal distribution, expression directionality, and sample clustering.

### Output Files Created
Running the script produces the following files in your working directory:
* **`Filtered_DEGs_Results.csv`** – Table of all differentially expressed genes ($|\log_2\text{FC}| > 5$) with mean expression values, fold changes, chromosomal annotations, and higher-expression phenotype labels.
* **`2a_DEGs_by_Chromosome.png`** – Histogram/bar chart showing the distribution of DEGs across chromosomes.
* **`2b_DEGs_by_Chromosome_Segregated.png`** – Grouped bar chart comparing chromosomal DEG counts separated by `Tumor` vs. `Normal` dominance.
* **`2c_DEG_Regulation_Percentages.png`** – Bar chart displaying the percentage of DEGs upregulated versus downregulated in Tumor samples.
* **`2d_Gene_Expression_Heatmap.png`** – Heatmap visualizing gene expression across samples.
* **`2e_Gene_Expression_Clustermap.png`** – Hierarchically clustered heatmap grouping samples and genes by expression similarity.

# S&P 500 Market Analysis and Stock Segmentation Using Adapted RFM

**Module:** 6BUIS017W CRM & CM With Business Intelligence  
**Institution:** University of Westminster  
**Student ID:** 2084703  
**GitHub Repository:** [S-P500_Stock_Analysis_CWK1](https://github.com/nemitha21/S-P500_Stock_Analysis_CWK1)

---
# Generative AI Declaration:
In accordance with the University of Westminster’s Academic Integrity Policy, I declare that Generative AI tools were used strictly for permitted support tasks, including debugging Python code, outlining the report structure, and proofreading for grammar and clarity. All analytical reasoning, critical evaluation, data interpretation, and final written content are my own independent work.

## Project Overview
This repository contains the complete data pipeline, analytical code, and reproducible outputs for the individual coursework assessing market analysis and stock segmentation. 

The project adapts the traditional **Recency, Frequency, Monetary (RFM)** framework—typically used in Customer Relationship Management (CRM)—to evaluate **S&P 500 stock trading activity**. By comparing clusters based on financial risk/return against clusters based on trading volume anomalies, the analysis provides actionable business intelligence insights for investment analysts and fintech stakeholders.

## Methodology & Key Features
The analysis is executed entirely in Python via Google Colab and covers the following key stages:

1. **Data Acquisition & Validation:** 
   - Extracted 503 S&P 500 constituents from Wikipedia.
   - Downloaded daily prices (Close, Adjusted Close, Volume) and the ^GSPC benchmark via `yfinance` (Jan 2021 – Dec 2024).
   - Applied strict validation rules (100% coverage, corporate action checks), resulting in **486 retained shares**.
2. **Feature Engineering:**
   - Calculated **Mean Weekly Return** and **Weekly Beta** (Risk/Return matrix).
   - Adapted **RFM Metrics**: Recency (calendar days to last high-volume event), Frequency (count of volume spikes in the final 60 sessions), and Monetary (approximate traded value). Explicit observation date: `2024-12-31`.
3. **Stock Segmentation (Clustering):**
   - Applied **Agglomerative (Ward)** and **K-Means** clustering to two distinct feature matrices.
   - Evaluated cluster counts ($k=2$ to $8$) using Silhouette scores, Inertia, and Adjusted Rand Index (ARI). Final selection: $k=5$ for all solutions.
4. **Sensitivity Analysis:**
   - Analyzed Pearson/Spearman correlations and Eta-squared ($\eta^2$) to determine feature influence.
   - Conducted a controlled sensitivity test by removing the Monetary feature to observe its impact on cluster stability and traded-value separation.
5. **Business Intelligence Design:**
   - Proposed a Star-Schema Data Mart design to support daily grain observations, derived metrics, and strict calculation provenance.

## Repository Structure
To ensure full reproducibility, the repository is organized into the following directories:

```text
├── data/
│   ├── raw/                # Raw data snapshots, Wikipedia scrape, and acquisition_metadata.json
│   └── clean/              # Validated daily prices, weekly returns, and high-volume event flags
├── outputs/
│   ├── figures/            # All required visualisations (Dendrograms, PCA, Silhouette plots, Sector lifts)
│   ├── *.csv               # Feature tables, cluster assignments, correlation matrices, and diagnostics
│   └── *.json              # Metadata files (RFM parameters, clustering seeds, feature preparation logs)
├── CRM_CW1_2084703.ipynb   # The main runnable Jupyter Notebook containing all analysis steps
├── requirements.txt        # Python package versions for environment replication
└── README.md               # This file

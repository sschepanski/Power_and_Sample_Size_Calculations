# GOODSENSE – Sample Size and Power Analysis

This folder contains the sample size and power analysis for a paired diagnostic accuracy study comparing canine olfactory testing with low-dose chest CT at a lung cancer center. Both index tests are performed on the same participants. Diagnostic truth (reference standard) is defined as histology-positive for cancer and benign histology or protocolized imaging follow-up (up to 24 months; double read; blinded to dog results) for non-cancer.

## Project Overview

The study is designed as a case-enriched accuracy study: we target required numbers within disease-status subgroups rather than relying on prevalence in an all-comers screen. The dog result must not influence verification decisions (to limit verification bias).

### Primary Objectives (co-primary)
1. Sensitivity non-inferiority (Dogs vs. CT) with a 5%-point margin.
2. Specificity superiority (Dogs vs. CT)
Each hypothesis is tested one-sided at α = 0.025 (alpha-splitting) with 80% power, using McNemar’s test on paired binary outcomes within the relevant subgroup (cancer for sensitivity, non-cancer for specificity).

## Contents

This folder includes two files:

- **SampleSize.R**: Main R script computing subgroup requirements via McNemar, plus utilities for discordance sensitivity analyses.
  
- **README.md**: This file, summarizing the project background, rationale behind the sample size calculation, and guidance for running the script and interpreting the results.

## Getting Started

To run the analysis, open the **SampleSize.ipynb** script in RStudio or any R console. The script requires the `pwr` package. It is fully annotated and walks through each step of the process, from defining effect size assumptions to computing adjusted sample sizes.

## Methodology

- Test comparison: McNemar’s test on paired 2×2 tables.
- Planning parameters: expressed via expected difference (Δ) and discordance (d).
    - For sensitivity (cancer subset): ΔSe=p01(D)−p10(D), dD=p01(D)+p10(D)
    - For specificity (non-cancer subset): ΔSp=p01(N)−p10(N), dN=p01(N)+p10(N)
- Planning formula (Normal approx., one-sided):
n≈(z1−α+z1−β)2 * (p01+p10) / [(p01−p10)−margin]2
with margin = −NI_margin for sensitivity NI, and margin = 0 for specificity superiority.

## Contact

For questions or further information about this project, please contact Dr. Steven Schepanski.

---

This repository documents a transparent and reproducible process for case-enriched diagnostic accuracy planning in a lung cancer setting, aligning operational recruitment with rigorous statistical targets.

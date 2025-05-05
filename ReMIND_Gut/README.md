# ReMIND-Gut Project – Sample Size and Power Analysis

This folder contains the sample size and power analysis for the **ReMIND-Gut** project, a randomized controlled trial investigating the effects of a structured meditation intervention on gut-brain interactions in healthy adults. The primary aim of this analysis is to determine the minimum sample size required to detect between-group differences in **short-chain fatty acid (SCFA)** levels, while adjusting for baseline SCFA concentrations using an ANCOVA model.

## Project Overview

**ReMIND-Gut** stands for *Regulating the Microbiome and Inflammation via Meditation*. This RCT explores how mindfulness-based practices can modulate the gut microbiome and its metabolites, with a particular focus on SCFAs. As part of a growing body of psychobiological research, the study investigates how mental training can influence mental health, inflammation, microbial composition, and metabolite production, thereby informing pathways along the gut-brain axis.

### Research Objectives
1. **Microbiome Regulation**: Assess changes in gut microbiota composition and metabolite profiles following a structured meditation intervention.
2. **SCFA Modulation**: Detect group differences in SCFA concentrations (e.g., iso-butyrate) at follow-up, adjusting for baseline levels.
3. **Inflammatory Markers**: Explore potential downstream effects on inflammatory biomarkers (e.g., CRP, IL-6, TNF-α).
4. **Gut-Brain Outcomes**: Examine associations between microbiome/metabolite shifts and psychological well-being measures (e.g., stress, mood, mindfulness).

## Contents

This folder includes two files:

- **SampleSize.R**: The primary R script for sample size and power analysis. It estimates the number of participants required to detect a statistically and clinically meaningful difference in SCFA concentrations between intervention and control groups, using ANCOVA. The analysis includes an adjustment for baseline covariates and accounts for a 20% dropout rate.
  
- **README.md**: This file, providing an overview of the ReMIND-Gut project, the rationale behind the sample size analysis, and guidance on interpreting results.

## Getting Started

To run the analysis, open the **SampleSize.R** script in RStudio or your preferred R environment. Ensure that required packages (e.g., `pwr`) are installed. The script is annotated to guide you through each step, from defining assumptions based on the literature (Raman et al., 2023) to computing adjusted effect sizes and sample sizes.

## Methodology

The sample size calculation is based on visual approximations from **Raman et al. (2023)** regarding iso-butyrate concentrations in meditators. A between-group difference of **0.006 micromolar proportions** was assumed, with a pooled standard deviation of **0.0131**, yielding a **Cohen’s d of 0.458**. This translates to an **adjusted Cohen’s f of 0.274** after accounting for baseline SCFA (assumed R² = 0.30). Using ANCOVA and targeting 80% power (α = 0.05), the required sample size is **54 participants per group**. After adjusting for 20% dropout, the final recommended sample size is **68 per group** (total N = 136).

Secondary analyses will explore mental health outcomes using similar power estimation techniques.

## Contact

For questions or further information about this project, please contact Dr. Steven Schepanski.

---

This repository aims to ensure transparency and reproducibility in sample size planning for the ReMIND-Gut trial, supporting the rigorous evaluation of meditation-based interventions on gut-brain health.

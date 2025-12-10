# Sample Size and Power Analysis

This folder contains the sample size and power analysis for a longitudinal mechanistic study investigating how maternal immune activation in late pregnancy and Hofbauer-cell phenotypes relate to early offspring temperament. The analytical framework combines latent maternal immune indices, functional and transcriptional Hofbauer-cell readouts, and repeated Infant Behavior Questionnaire (IBQ-R) assessments to model developmental pathways.

## Project Overview

The power analysis focuses on the key hypothesis underlying Objective 3:
variation in maternal immune activation (MIA) and Hofbauer-cell phagocytic function predicts individual differences in early offspring temperament. Because the full analytical strategy uses latent growth curve modelling (LGCM) and structural equation models (SEM), the sample size calculation relies on a simplified and conservative regression-based formulation using a continuous 24-month temperament score as the primary endpoint. This approach is standard practice in mechanistic cohort studies and provides a defensible lower bound for the required analyzable sample.

### Primary Power Target
1. Outcome: IBQ-R orienting/regulation score at 24 months (continuous).
2. Predictor block: latent MIA score, Hofbauer-cell phagocytic index, and their interaction.
3. Covariates: maternal age and pre-pregnancy BMI.
4. Effect size assumption: small-to-moderate incremental effect (Cohen’s f² ≈ 0.045), derived conservatively from published effect sizes linking maternal inflammation to IBQ-based temperament.
5. Statistical test: multiple regression / single-path SEM approximation.
6. Criteria: α = 0.05 (two-sided), power = 0.80.

The resulting analyzable sample requirement is then adjusted for expected attrition, using empirical retention estimates from the parent cohort.

## Contents

This folder includes two files:

- **SampleSize.R**: Main R script performing the sample size calculation using the published pwr package.
  
- **README.md**: This file, summarizing the project background, rationale behind the sample size calculation, and guidance for running the script and interpreting the results.

## Getting Started

To run the analysis, open the **SampleSize.ipynb** script in RStudio or any R console. The script requires the `pwr` package. It is fully annotated and walks through each step of the process, from defining effect size assumptions to computing adjusted sample sizes.


## Contact

For questions or further information about this project, please contact Dr. Steven Ngandeu Schepanski.

---

This repository documents a transparent, reproducible sample size determination tailored to a mechanistic human developmental immunology project, aligning statistical planning with the study’s translational objectives and operational feasibility.

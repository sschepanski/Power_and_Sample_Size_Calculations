# MindSpaceOne 2.0 – Sample Size and Power Analysis

This folder contains the sample size and power analysis for the **MindSpaceOne 2.0 project**, a randomized controlled trial investigating the effects of a digital, self-guided hypnotherapy and aromatherapy intervention on subjective relaxation and psychophysiological regulation in healthy adults. The primary aim of this analysis is to determine the minimum sample size required to detect between-group differences in subjective relaxation (MDBF-RU), while adjusting for baseline levels using an ANCOVA model.

## Project Overview

**MindSpaceOne 2.0** is a follow-up to the successful MindSpaceOne 1.0 study. It investigates the potential of aroma-supported hypnotherapeutic interventions to elicit psychophysiological downregulation, both acutely and in conditioned form. The study examines effects on subjective well-being and relaxation, with subgroups planned for secondary analysis to evaluate potential conditioned responses to aromatherapeutic stimuli.

### Research Objectives
1. **Immediate Relaxation Effects:** Evaluate the acute effects of guided hypnotherapy with or without aromatherapy on perceived relaxation.
2. **Conditioning Effects:** Assess whether repeated pairing of hypnotic and olfactory stimuli leads to conditioned relaxation responses.
3. **Intervention Optimization:** Compare two different essential oils (Lavender vs. Bergamot) and control for unspecific olfactory effects via cross-over designs.
4. **Subgroup Differentiation:** Investigate differential outcomes in later subgroups, derived from the two main aroma groups.

## Contents

This folder includes two files:

- **SampleSize.R**: The primary R script for sample size and power analysis. It estimates the number of participants required to detect statistically meaningful group differences using ANCOVA. The script adjusts for baseline covariates and accounts for an anticipated 35% dropout rate. In addition, the sample size for two groups is doubled to account for planned subgroup splitting in later study phases.
  
- **README.md**: This file, summarizing the project background, rationale behind the sample size calculation, and guidance for running the script and interpreting the results.

## Getting Started

To run the analysis, open the **SampleSize.ipynb** script in RStudio or any R console. The script requires the `pwr` package. It is fully annotated and walks through each step of the process, from defining effect size assumptions to computing adjusted sample sizes.

## Methodology

The sample size calculation is based on observed effect sizes from the **MindSpaceOne 1.0 study**. Specifically, Cohen’s d values of **0.33–0.49** were reported for group differences in the primary outcome (MDBF-RU). A conservative average was converted to Cohen’s f = 0.175, which was then adjusted to f = 0.196 assuming 20% of variance is explained by baseline scores **(R² = 0.20)**. Using ANCOVA with four groups, α = 0.05, and 80% power, this results in a required sample size of 73 participants per group (before dropout).

To account for an expected **35% dropout**, the sample size increases to 105 per group. Since two of the four study arms will be split into subgroups in later phases, their required sample size is doubled to preserve adequate power for subgroup analysis. This results in a total target sample size of **630 participants**.

## Contact

For questions or further information about this project, please contact Dr. Steven Schepanski.

---

This repository aims to ensure transparency and reproducibility in sample size planning for the MindSpaceOne 2.0 trial, supporting the rigorous evaluation of self-administered hypnosis and essential oil-based interventions on mental health.

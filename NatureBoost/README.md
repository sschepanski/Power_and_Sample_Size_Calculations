# NatureBoost Project - Sample Size and Power Analysis

This folder contains the sample size and power analysis for the **NatureBoost** project, a research study investigating the impact of nature-based interventions on sleep quality and well-being in long-term care residents. The analysis focuses on determining the minimum sample size needed to detect statistically significant effects of the interventions, with consideration of relevant covariates and an anticipated attrition rate.

## Project Overview

The NatureBoost project aims to assess the effects of immersive nature-based experiences—such as forest scents, VR visuals, and natural sounds—on sleep quality and overall well-being among elderly residents in long-term care facilities. Given the unique study population, sample size calculations account for factors such as potential challenges with technology use and higher-than-average dropout rates.

## Contents

This folder contains two files:

- **SampleSize.ipynb**: The main Jupyter notebook for the sample size and power analysis of the NatureBoost project. This notebook:
  - Utilizes a simulation-based approach to calculate the required sample size for achieving a target power.
  - Incorporates covariates (e.g., baseline sleep quality, age, medication use) to adjust for initial differences among participants.
  - Applies an attrition rate of 40% to account for potential dropouts due to the advanced age and mobility limitations of participants.

- **README.md**: This file, providing an overview of the NatureBoost project, the purpose of the sample size analysis, and instructions for interpreting the results.

## Getting Started

To run the analysis, open the **SampleSize.ipynb** notebook in R and follow the instructions within each cell. Ensure all required R packages are installed, as listed in the notebook's setup section.

## Methodology

The sample size calculation is based on the primary outcome, the Pittsburgh Sleep Quality Index (PSQI), with secondary outcomes that include well-being, loneliness, mood, and cognitive function. A mixed linear model (ANCOVA) approach is used, controlling for baseline PSQI and other covariates. The notebook includes sensitivity analyses to test the robustness of the results.

## Contact

For questions or further information about this project, please contact Dr. Steven Schepanski.

---

This repository aims to make the sample size and power calculation approach for the NatureBoost project transparent and reproducible for future reference and further research.

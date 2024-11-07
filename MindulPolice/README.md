# MindfulPolice Project - Sample Size and Power Analysis

This folder contains the sample size and power analysis for the **MindfulPolice** project, a research study focused on designing and evaluating a mindfulness intervention specifically tailored for police officers. The analysis aims to determine the minimum sample size needed to detect statistically significant effects of the intervention, taking into account relevant covariates and an anticipated attrition rate.

## Project Overview

The MindfulPolice project seeks to assess the impact of a mindfulness-based intervention on police officers' mindfulness levels, as measured by the German version of the "Five Facet Mindfulness Questionnaire (FFMQ-D)." The study is designed with three time points: T0 (baseline), T1 (post-intervention), and T2 (four months post-intervention). Sample size calculations account for the unique characteristics of the target population, including potential challenges related to intervention adherence and dropout rates.

## Contents

This folder contains two files:

- **SampleSize.ipynb**: The main Jupyter notebook for the sample size and power analysis of the MindfulPolice project. This notebook:
  - Utilizes a simulation-based approach to calculate the required sample size for achieving a target power.
  - Adjusts for baseline measures and includes covariates such as age, sex, and other relevant demographic factors.
  - Applies an estimated attrition rate to accommodate potential participant dropouts over the course of the study.

- **README.md**: This file, providing an overview of the MindfulPolice project, the purpose of the sample size analysis, and instructions for interpreting the results.

## Getting Started

To run the analysis, open the **SampleSize.ipynb** notebook in R and follow the instructions within each cell. Ensure all required R packages are installed, as listed in the notebook's setup section.

## Methodology

The sample size calculation focuses on the primary outcome, the FFMQ-D, and will analyze the five facets of mindfulness at T1, adjusting for baseline scores at T0. A mixed linear model (ANCOVA) approach is used, with additional covariates such as age and sex to control for individual differences. The notebook also includes sensitivity analyses to evaluate the robustness of the results.

## Contact

For questions or further information about this project, please contact Dr. Steven Schepanski.

---

This repository aims to ensure that the sample size and power calculation approach for the MindfulPolice project is transparent and reproducible for future reference and further research.

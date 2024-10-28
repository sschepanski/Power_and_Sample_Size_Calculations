# HappyKraut Project - Sample Size and Power Analysis

This folder contains the sample size and power analysis for the **HappyKraut** project, a randomized, double-blind, placebo-controlled trial investigating the effects of daily sauerkraut consumption on seasonal allergies, systemic inflammation, and immune responses in adolescents and young adults. The primary goal of this analysis is to determine the sample size required to detect clinically meaningful differences between the intervention (sauerkraut) and control (placebo) groups in the severity of allergy symptoms.

## Project Overview

The HappyKraut project seeks to assess the therapeutic potential of fermented foods, specifically sauerkraut, on seasonal allergies. Seasonal allergic rhinitis, commonly known as hay fever, involves immune-mediated responses to airborne allergens, with symptoms like nasal congestion, sneezing, and eye irritation. Existing research suggests that the human microbiome plays a role in immune modulation, potentially influencing allergic diseases. This study aims to build upon this knowledge by exploring whether regular sauerkraut consumption can alleviate allergy symptoms and reduce inflammatory markers.

### Research Objectives
1. **Symptom Reduction**: Determine if daily sauerkraut intake reduces the severity and frequency of allergy symptoms, measured using the Total Nose and Eye Symptom Score (TNESS).
2. **Immune Response Modulation**: Examine changes in immune cell activity, including eosinophils, mast cells, and T cells, as well as specific cytokines (e.g., IL-6, IL-10, CRP).
3. **Systemic Inflammation**: Assess reductions in systemic inflammation as indicated by biomarkers in blood samples.

## Contents

This folder includes two files:

- **SampleSize.ipynb**: The primary notebook for sample size and power analysis, utilizing a simulation-based approach to estimate the required sample size for achieving 80% power to detect differences in allergy symptom severity between groups. The analysis also incorporates a 20% attrition rate to account for potential dropouts.
  
- **README.md**: This file, providing an overview of the HappyKraut project, the purpose of the sample size analysis, and instructions for interpreting the results.

## Getting Started

To run the analysis, open the **SampleSize.ipynb** notebook in R and follow the step-by-step instructions within each cell. Ensure all necessary R packages are installed, as outlined in the notebook's setup section.

## Methodology

The sample size calculation focuses on the primary outcome, the TNESS questionnaire score, as a measure of symptom severity in seasonal allergies. A power analysis was performed to determine the minimum sample size needed to detect significant differences between the intervention and control groups, adjusting for a 20% attrition rate to account for dropouts. Secondary outcomes, including immune response modulation and inflammatory biomarkers, will be analyzed using similar methodologies to explore the broader impact of sauerkraut on immune function.

## Contact

For questions or further information about this project, please contact Dr. Steven Schepanski.

---

This repository aims to make the sample size and power calculations for the HappyKraut project accessible and transparent, supporting reproducibility and further research.

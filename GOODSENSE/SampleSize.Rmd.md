# Table of Content

- [Table of Content](#table-of-content)
- [0-General](#0-general)
- [1-Sample Size Calculation](#1--sample-size-calculation)
- [2-Conclusion](#2-conclusion)

# 0-General
[Back to Table of Content](#table-of-content)

# Sample Size Calculation for GOODSENSE

## Introduction
[Back to Table of Content](#table-of-content)

This sample size calculation determines the minimum numbers of cancer and non-cancer participants required in a paired diagnostic accuracy study comparing CT with canine olfactory testing at a lung cancer center. Both index tests are performed on the same participants; diagnostic truth is established by an independent reference standard: histology positive for cancer, and benign histology or protocolized imaging follow-up (up to 24 months; double read, blinded to dog results) for non-cancer. The dog result must not influence verification decisions.

### Primary objectives (co-primary):
1. Sensitivity non-inferiority (dogs vs. CT) with a 5 percentage-point margin;
2. Specificity superiority (dogs vs. CT).

Both hypotheses are tested with one-sided α = 0.025 (alpha-splitting) and 80% power using McNemar’s test on paired binary outcomes within the relevant subgroups (cancer for sensitivity; non-cancer for specificity). The design is case-enriched (we target required numbers within each subgroup rather than relying on prevalence).

## Planning assumptions and resulting analytical sample
- Discordance (cancer, for sensitivity): dD=0.12 (i.e., 12% of cancer cases yield different dog vs. CT classifications).
- Expected sensitivity difference (Dog – CT): 0 (equal sensitivity anticipated).
- Non-inferiority margin (sensitivity): 0.05 (dogs may be at most 5 percentage points less sensitive than CT)
- Discordance (non-cancer, for specificity): dN=0.15.
- Expected specificity difference (Dog – CT): +0.10 (dogs 10 percentage points more specific).

# 1- Sample Size Calculation
[Back to Table of Content](#table-of-content)


```R
###############################################################
# Sample size planning for a paired diagnostic accuracy study
# Comparing Dogs vs. CT using an independent reference standard
# (Histology+/− and/or protocolized follow-up for non-cancer)
#
# Primary endpoints (two one-sided tests):
#   1) Sensitivity: Non-inferiority of Dogs vs. CT among cancer cases
#   2) Specificity: Superiority of Dogs vs. CT among non-cancer cases
#
# Method: McNemar test for paired binary outcomes (one-sided)
#
# Core inputs you must set:
#   alpha_one_sided  : one-sided alpha per primary test (e.g., 0.025 if alpha-splitting)
#   power            : target power (e.g., 0.80)
#   d_D              : discordance among diseased (cancer) cases for Se comparison
#   d_N              : discordance among non-diseased (non-cancer) cases for Sp comparison
#   DeltaSe_exp      : expected Se difference (Dog - CT) among cancer cases (often ~0)
#   NI_margin_Se     : non-inferiority margin for sensitivity (e.g., 0.05 = 5 percentage points)
#   DeltaSp_exp      : expected Sp difference (Dog - CT) among non-cancer cases (e.g., +0.10)
#
# Definitions (paired 2x2 within each subgroup):
#   Let b = Dog positive, CT negative   (Dog "better" on that person)
#   Let c = Dog negative, CT positive   (CT "better"  on that person)
#   Discordance d = b + c     (as a proportion within the subgroup)
#   Expected difference Delta = b - c   (Dog - CT)
#
# Planning formula (Normal approximation for McNemar, one-sided):
#   n ≈ ((z_{1-α} + z_{1-β})^2 * (p01 + p10)) / (((p01 - p10) - margin)^2)
# where:
#   - For Se non-inferiority: margin = -NI_margin_Se (H0: Delta ≤ -NI_margin_Se)
#   - For Sp superiority    : margin = 0            (H0: Delta ≤ 0)
#
# n denotes the required number of PAIRED subjects in the respective subgroup:
#   - n_cancer     : number of cancer cases needed for Se non-inferiority
#   - n_noncancer  : number of non-cancer cases needed for Sp superiority
# Total planned N in a case-enriched design is n_cancer + n_noncancer.
###############################################################

# ---------- Helper functions ----------

# Normal Z quantile
zq <- function(p) qnorm(p)

# Derive p01 and p10 from total discordance (d) and expected difference (Delta)
# Constraints:
#   d = p01 + p10  (must satisfy d ≥ |Delta|)
#   Delta = p01 - p10
# Hence:
#   p01 = (d + Delta)/2
#   p10 = (d - Delta)/2
p01_p10_from_d_Delta <- function(d, Delta) {
  if (d < abs(Delta)) {
    stop("Invalid combination: discordance d must be >= |Delta|.")
  }
  p01 <- (d + Delta) / 2
  p10 <- (d - Delta) / 2
  if (p01 < 0 || p10 < 0) {
    stop("Invalid p01/p10 (negative). Check d and Delta.")
  }
  c(p01 = p01, p10 = p10)
}

# Core function: one-sided McNemar sample size
# H0: (p01 - p10) <= margin   (we plan n to reject H0 with given power)
n_mcnemar_one_sided <- function(p01, p10, alpha_one_sided = 0.025, power = 0.80, margin = 0) {
  # Expected "distance" from the null boundary:
  #   effect = (p01 - p10) - margin
  effect <- (p01 - p10) - margin
  if (effect <= 0) {
    stop("Expected difference <= margin. No power under these assumptions.")
  }
  # Total discordance:
  disc <- p01 + p10
  # Z factor for one-sided alpha and power:
  zsum_sq <- (zq(1 - alpha_one_sided) + zq(power))^2
  # Sample size (rounded up):
  n <- (zsum_sq * disc) / (effect^2)
  ceiling(n)
}

# Compute n_cancer and n_noncancer using interpretable inputs
sample_size_paired <- function(
  # global settings
  alpha_one_sided = 0.025,
  power = 0.80,
  # Sensitivity (among cancer): Non-inferiority
  d_D,                  # discordance among diseased (cancer) cases
  DeltaSe_exp = 0.00,   # expected Se difference (Dog - CT)
  NI_margin_Se = 0.05,  # non-inferiority margin (0.05 = 5 pct points)
  # Specificity (among non-cancer): Superiority
  d_N,                  # discordance among non-diseased (non-cancer) cases
  DeltaSp_exp = 0.10    # expected Sp difference (Dog - CT)
) {
  # 1) Sensitivity non-inferiority (cancer subset)
  #    H0: (p01 - p10) <= -NI_margin_Se  --> margin = -NI_margin_Se
  pars_D <- p01_p10_from_d_Delta(d = d_D, Delta = DeltaSe_exp)
  n_cancer <- n_mcnemar_one_sided(
    p01 = pars_D["p01"], p10 = pars_D["p10"],
    alpha_one_sided = alpha_one_sided, power = power,
    margin = -NI_margin_Se
  )

  # 2) Specificity superiority (non-cancer subset)
  #    H0: (p01 - p10) <= 0              --> margin = 0
  pars_N <- p01_p10_from_d_Delta(d = d_N, Delta = DeltaSp_exp)
  n_noncancer <- n_mcnemar_one_sided(
    p01 = pars_N["p01"], p10 = pars_N["p10"],
    alpha_one_sided = alpha_one_sided, power = power,
    margin = 0
  )

  # Total (case-enriched): sum of subgroup requirements
  N_total <- n_cancer + n_noncancer

  list(
    inputs = list(
      alpha_one_sided = alpha_one_sided,
      power = power,
      d_D = d_D, DeltaSe_exp = DeltaSe_exp, NI_margin_Se = NI_margin_Se,
      d_N = d_N, DeltaSp_exp = DeltaSp_exp
    ),
    derived = list(
      p01_p10_D = pars_D,
      p01_p10_N = pars_N
    ),
    results = list(
      n_cancer = n_cancer,
      n_noncancer = n_noncancer,
      N_total = N_total
    )
  )
}
```


```R
# Print
print_ss <- function(ss) {
  cat("------------------------------------------------------------\n")
  cat("Sample size planning (paired McNemar tests)\n")
  cat("One-sided alpha:", ss$inputs$alpha_one_sided, " | Power:", ss$inputs$power, "\n\n")

  cat("Sensitivity (Non-inferiority, among cancer cases):\n")
  cat("  Discordance d_D:", ss$inputs$d_D, "\n")
  cat("  Expected ΔSe (Dog - CT):", ss$inputs$DeltaSe_exp, "\n")
  cat("  NI margin (Se):", ss$inputs$NI_margin_Se, "\n")
  cat("  -> p01_D:", round(ss$derived$p01_p10_D["p01"], 4),
      " | p10_D:", round(ss$derived$p01_p10_D["p10"], 4), "\n")
  cat("  Required cancer cases (n_cancer):", ss$results$n_cancer, "\n\n")

  cat("Specificity (Superiority, among non-cancer cases):\n")
  cat("  Discordance d_N:", ss$inputs$d_N, "\n")
  cat("  Expected ΔSp (Dog - CT):", ss$inputs$DeltaSp_exp, "\n")
  cat("  -> p01_N:", round(ss$derived$p01_p10_N["p01"], 4),
      " | p10_N:", round(ss$derived$p01_p10_N["p10"], 4), "\n")
  cat("  Required non-cancer cases (n_noncancer):", ss$results$n_noncancer, "\n\n")

  cat("TOTAL (case-enriched): N_total =", ss$results$N_total, "\n")
  cat("------------------------------------------------------------\n")
}
```


```R
# ---------- Main script ----------
alpha_one_sided <- 0.025  # one-sided per primary test (alpha-splitting)
power           <- 0.80

d_D          <- 0.08      # discordance among cancer cases (for Se comparison)
DeltaSe_exp  <- 0.00      # expected Se difference (Dog - CT)
NI_margin_Se <- 0.05      # NI margin (max 5 pct points worse accepted)

d_N          <- 0.15      # discordance among non-cancer cases (for Sp comparison)
DeltaSp_exp  <- 0.10      # expected Sp difference (Dog - CT)

# Compute sample sizes
ss <- sample_size_paired(
  alpha_one_sided = alpha_one_sided,
  power = power,
  d_D = d_D, DeltaSe_exp = DeltaSe_exp, NI_margin_Se = NI_margin_Se,
  d_N = d_N, DeltaSp_exp = DeltaSp_exp
)

print_ss(ss)
```

    ------------------------------------------------------------
    Sample size planning (paired McNemar tests)
    One-sided alpha: 0.025  | Power: 0.8 
    
    Sensitivity (Non-inferiority, among cancer cases):
      Discordance d_D: 0.08 
      Expected <U+0394>Se (Dog - CT): 0 
      NI margin (Se): 0.05 
      -> p01_D: 0.04  | p10_D: 0.04 
      Required cancer cases (n_cancer): 252 
    
    Specificity (Superiority, among non-cancer cases):
      Discordance d_N: 0.15 
      Expected <U+0394>Sp (Dog - CT): 0.1 
      -> p01_N: 0.125  | p10_N: 0.025 
      Required non-cancer cases (n_noncancer): 118 
    
    TOTAL (case-enriched): N_total = 370 
    ------------------------------------------------------------


With a one-sided significance level of 0.025 for each primary hypothesis and a target power of 80%, the planned design requires 252 cancer cases to demonstrate that dogs are not more than five percentage points less sensitive than CT, assuming equal true sensitivity and an 8% discordance rate between the two methods. In this cancer subgroup, the discordance is split evenly between cases where the dog is correct and the CT is wrong, and vice versa, reflecting an expectation of similar diagnostic accuracy. For the non-cancer subgroup, where the aim is to show a ten percentage point advantage in specificity for the dogs, a higher discordance rate of 15% is assumed, with most disagreements favoring the dog. Under these assumptions, 118 non-cancer cases are needed. Taken together, the total case-enriched sample size amounts to 370 paired subjects.


```R
# ---------- Sensitivity grid over discordance values ----------

sensitivity_grid <- function(
  dD_vec = c(0.05, 0.08, 0.12),
  dN_vec = c(0.10, 0.15, 0.20),
  alpha_one_sided = 0.025, power = 0.80,
  DeltaSe_exp = 0.00, NI_margin_Se = 0.05,
  DeltaSp_exp = 0.10
) {
  out <- expand.grid(d_D = dD_vec, d_N = dN_vec, KEEP.OUT.ATTRS = FALSE, stringsAsFactors = FALSE)
  out$n_cancer <- NA_integer_
  out$n_noncancer <- NA_integer_
  out$N_total <- NA_integer_
  for (i in seq_len(nrow(out))) {
    res <- sample_size_paired(
      alpha_one_sided = alpha_one_sided, power = power,
      d_D = out$d_D[i], DeltaSe_exp = DeltaSe_exp, NI_margin_Se = NI_margin_Se,
      d_N = out$d_N[i], DeltaSp_exp = DeltaSp_exp
    )$results
    out$n_cancer[i] <- res$n_cancer
    out$n_noncancer[i] <- res$n_noncancer
    out$N_total[i] <- res$N_total
  }
  out[order(out$d_D, out$d_N), ]
}

# Output
grid_res <- sensitivity_grid()
print(grid_res)
```

       d_D  d_N n_cancer n_noncancer N_total
    1 0.05 0.10      157          79     236
    4 0.05 0.15      157         118     275
    7 0.05 0.20      157         157     314
    2 0.08 0.10      252          79     331
    5 0.08 0.15      252         118     370
    8 0.08 0.20      252         157     409
    3 0.12 0.10      377          79     456
    6 0.12 0.15      377         118     495
    9 0.12 0.20      377         157     534


The sensitivity analysis illustrates how strongly the required sample size depends on the assumed discordance rates between dogs and CT in each subgroup. Lower discordance rates lead to smaller required sample sizes, while higher rates increase the number of participants needed. The most conservative scenario (line 9), with a discordance of 12% among cancer cases and 20% among non-cancer cases, results in the largest calculated sample size: 377 cancer cases and 157 non-cancer cases, for a total of 534 paired subjects. This scenario assumes that the two tests disagree relatively often, **about one in eight cancer cases and one in five non-cancer cases**, and that these disagreements are split according to the expected differences in accuracy. Under such conditions, the study would require more than one year of recruitment if the lung cancer center screens approximately 500 individuals annually, particularly because not all screened individuals will meet the inclusion criteria or have complete follow-up. In practice, using more moderate discordance rates (such as those in the main analysis with 12% and 15%) would reduce the required total to 495, which is more achievable within a single year.


```R
# ---------- Inflate non-cancer recruitment for follow-up losses ----------

# If some non-cancer cases have NO benign histology and require follow-up,
# and some of those will not complete follow-up, means we need to inflate recruitment accordingly
inflate_for_followup <- function(n_noncancer_needed,
                                prop_with_benign_histology,
                                followup_complete_rate) {
  # prop_without_histology is implied
  prop_without_histology <- 1 - prop_with_benign_histology
  # Overall usable rate among recruited non-cancer cases
  usable_rate <- prop_with_benign_histology +
                 prop_without_histology * followup_complete_rate
  # Required recruits to achieve the analyzable target
  recruits <- ceiling(n_noncancer_needed / usable_rate)
  list(usable_rate = usable_rate, recruits = recruits)
}

# Build a sensitivity grid over input vectors
build_followup_grid <- function(n_noncancer_needed,
                                benign_histology_vec = seq(0.30, 0.60, by = 0.05),
                                followup_complete_vec = seq(0.70, 0.95, by = 0.05)) {
  grid <- expand.grid(
    prop_benign_histology = benign_histology_vec,
    followup_complete     = followup_complete_vec,
    KEEP.OUT.ATTRS = FALSE, stringsAsFactors = FALSE
  )
  grid$usable_rate <- NA_real_
  grid$recruits    <- NA_integer_

  for (i in seq_len(nrow(grid))) {
    res <- inflate_for_followup(
      n_noncancer_needed       = n_noncancer_needed,
      prop_with_benign_histology = grid$prop_benign_histology[i],
      followup_complete_rate     = grid$followup_complete[i]
    )
    grid$usable_rate[i] <- res$usable_rate
    grid$recruits[i]    <- res$recruits
  }

  # Output
  grid$benign_histology_pct <- paste0(round(100 * grid$prop_benign_histology), "%")
  grid$followup_complete_pct <- paste0(round(100 * grid$followup_complete), "%")
  grid$usable_rate_pct <- paste0(round(100 * grid$usable_rate), "%")

  # Sort for readability
  grid[order(grid$prop_benign_histology, grid$followup_complete), ]
}

```


```R
# Use analyzable non-cancer requirement from the main SS result
n_needed_noncancer <- ss$results$n_noncancer

grid_res <- build_followup_grid(
  n_noncancer_needed   = n_needed_noncancer,
  benign_histology_vec = c(0.30, 0.40, 0.50, 0.60),
  followup_complete_vec = c(0.60, 0.70, 0.80, 0.90)
)

# View
print(grid_res[, c("benign_histology_pct", "followup_complete_pct",
                   "usable_rate_pct", "recruits")],
      row.names = FALSE)

```

     benign_histology_pct followup_complete_pct usable_rate_pct recruits
                      30%                   60%             72%      164
                      30%                   70%             79%      150
                      30%                   80%             86%      138
                      30%                   90%             93%      127
                      40%                   60%             76%      156
                      40%                   70%             82%      144
                      40%                   80%             88%      135
                      40%                   90%             94%      126
                      50%                   60%             80%      148
                      50%                   70%             85%      139
                      50%                   80%             90%      132
                      50%                   90%             95%      125
                      60%                   60%             84%      141
                      60%                   70%             88%      135
                      60%                   80%             92%      129
                      60%                   90%             96%      123


This grid shows, for a fixed analytical target of 118 usable non-cancer cases, how many non-cancer participants you must recruit under different assumptions about how “non-cancer” is confirmed. Two factors drive the usable fraction: the share with benign histology (immediately usable) and the follow-up completion rate among those without histology. Across scenarios, the usable rate ranges from 72% to 96%, translating into recruitment needs between 164 and 123 non-cancer participants, respectively.

A realistic base case in a lung cancer center is to assume that about half of non-cancer determinations come from benign histology and half from protocolized follow-up, with ~80% of the follow-up arm completing verification. That corresponds to the 50% / 80% cell: a 90% usable rate and 132 non-cancer recruits to achieve 118 analyzable.

# 2-Conclusion
[Back to Table of Content](#table-of-content)

Under your primary planning assumptions (one-sided α=0.025, power=0.80, sensitivity non-inferiority margin=5 % points, expected 
ΔSe=0, expected ΔSp=+10 points), the analytical (i.e., paired, usable) sample size is:
- Cancer (for sensitivity NI): n cancer = 377
- Non-cancer (for specificity superiority): n non-cancer = 118
- Analytical total: N = 495

Because a proportion of non-cancer determinations will rely on follow-up (and not all of those will complete), we inflate non-cancer recruitment using a neutral, defensible base case of 50% benign histology and 80% follow-up completion among those without histology:

usable rate=0.50+0.50×0.80=0.90 ==> recruit [118/0.90] = 132 non-cancer participants.

Cancer cases use histology and do not need this verification inflation, so recruitment there targets the analytical need of 377.

Putting this together before any general failures results to 509 participants. Finally, apply a realistic technical/procedural failure buffer (e.g. unusable specimen, protocol deviations) via a pragmatic +10%, the total sample size is 560.

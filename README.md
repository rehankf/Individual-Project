# Markov Chain-Based Degradation Modelling and Machine Learning Health State Classification for Power Transformers Using Dissolved Gas Analysis 

---

## Introduction

This project develops two complementary probabilistic approaches to transformer condition assessment and lifetime prediction:

1. **Markov degradation model** - A 5-state absorbing Markov chain models population-level transformer degradation over 40 year service lives. Maximum likelihood estimation (MLE) validates transition matrix recovery from observed state sequences to calculate mean remaining useful life and survival probability

2. **Machine learning health state classification** - Logistic regression and random forest classifiers predict individual transformer health states from synthetic dissolved gas analysis (DGA) data grounded in real-world gas concentration thresholds

---

## Contextual Overview


**Data flow:**
- Markov model: Simulated transformer histories -> state transition counts -> estimated P matrix -> RUL/survival curves
- ML model: Synthetic DGA samples -> trained classifier -> predicted health state

All code is implemented in Jupyter notebook using Python with NumPy, pandas, matplotlib, seaborn, and scikit-learn.

---

## Installation Instructions

### Prerequisites
- JupyterLite (browser-based)

### Environment Setup
1. Navigate to https://jupyter.org/try-jupyter/lab/
2. Upload `ProjectNEW_25_.ipynb`
3. All required libraries are pre-installed

--- 

## How to Run the Software
Execute all cells sequentually in Jupyter from Run -> Run All Cells 

---

## Technical Details

### Markov Chain Model

**Estimation:** Maximum Likelihood Estimator (MLE) for transition probabilities:

P̂_ij = n_ij / n_i

where n_ij = observed transitions from state i to j, n_i = total visits to state i.

**Remaining Useful Life:** Computed via fundamental matrix N = (I − Q)⁻¹, where Q is the transient-to-transient 4x4 sub-matrix of P. RUL from state i is the sum of row i of N.

**Survival Function:** S(t) = 1 − [H₀·Pᵗ]_VeryPoor, the probability of not yet reaching the absorbing state by year t.

### Synthetic DGA Data

**Gas concentrations:** 7 features (H₂, CH₄, C₂H₆, C₂H₄, C₂H₂, CO, CO₂) sampled from multivariate normal distributions:

- **Means:** Per-state values calibrated to IEEE C57.104-2019 typical concentrations
- **Covariance:** Derived from fault-gas correlations
- **Noise:** 15% measurement noise simulates real DGA sampling variability

**Sample size:** 200 samples per state (1000 total), split 80/20 for training/testing

### Machine Learning Classifiers

**Logistic Regression:**
- Standardised input features (zero mean, unit variance)

**Random Forest:**
- 50 trees, max depth 5, min samples per split 2

---

## Known Issues and Future Improvements

### Known Limitations

1. **Synthetic data only** — Reported classification accuracies (95-97%) are optimistic.

2. **Time-homogeneous Markov chain** - Transition probabilities are time-constant. In reality, degradation accelerates with age, loading stress, and environmental factors

### Planned Improvements

**Extended feature set** - Investigate furan analysis (paper insulation degradation) and frequency response analysis (FRA)

---

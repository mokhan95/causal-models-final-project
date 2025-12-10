# Causal Effect of Advertising on Conversion

**Course:** Causal Models in Data Science
**Author:** Mohammad (Mo) Khan
**Date:** December 2025

## Overview

This project estimates the causal effect of online advertising exposure on user conversion using the Criteo Uplift Modeling Dataset (~14 million users). We use randomized treatment assignment as an instrumental variable to address selection bias from non-random ad exposure.

**Key Finding:** Ad exposure increases conversion probability by approximately 2.8–3.0 percentage points for compliers, roughly doubling their conversion rate.

## Repository Structure

```
submission/
├── README.md                 # This file
├── causal_analysis.ipynb     # Main analysis notebook
└── data/
    └── criteo-research-uplift-v2.1.csv.gz  # Dataset
```

## Requirements

- Python 3.8+
- Jupyter Notebook

### Dependencies

```
numpy
pandas
matplotlib
seaborn
statsmodels
scikit-learn
econml
dowhy
```

## How to Reproduce

### Step 1: Clone the Repository

```bash
git clone https://github.com/mokhan95/causal-models-final-project.git
cd causal-models-final-project
```

### Step 2: Install Dependencies

```bash
pip install numpy pandas matplotlib seaborn statsmodels scikit-learn econml dowhy
```

### Step 3: Download Data (if not included)

The Criteo Uplift Modeling Dataset should be in `data/criteo-research-uplift-v2.1.csv.gz`. If not present, download from:
- [Criteo AI Lab](https://ailab.criteo.com/criteo-uplift-prediction-dataset/)

### Step 4: Run the Analysis

Open and run `causal_analysis.ipynb` in Jupyter:

```bash
jupyter notebook causal_analysis.ipynb
```

Run all cells sequentially. The notebook contains:

| Section | Description | Runtime |
|---------|-------------|---------|
| 1. Data Loading | Load and preprocess 14M observations | ~30 sec |
| 2. EDA | Exploratory data analysis and figures | ~1 min |
| 3. IV/2SLS | Two-stage least squares estimation | ~2 min |
| 4. DML-IV | Double ML with instrumental variables (500K sample) | ~5 min |
| 5. Evaluation | DoWhy refutation tests (500K sample) | ~1 min |

**Total runtime:** ~10 minutes

## Methods

### Method 1: Instrumental Variables (IV/2SLS)
- Uses randomized treatment assignment (Z) as instrument for ad exposure (D)
- Estimates Local Average Treatment Effect (LATE) for compliers
- **Result:** 2.82 pp (95% CI: 2.63–3.01)

### Method 2: Double Machine Learning with IV (DML-IV)
- Flexible ML-based covariate adjustment using Random Forest
- Cross-fitting to prevent overfitting bias
- **Result:** 2.99 pp (95% CI: 2.98–3.00)

### Evaluation: Refutation Tests
- Placebo Treatment Test: Effect disappears with random treatment 
- Data Subset Test: Estimate stable on 80% of data 
- Random Common Cause Test: Robust to simulated confounders 

## Data

**Source:** Criteo Uplift Modeling Dataset (Diemert et al., 2018)

| Variable | Type | Description |
|----------|------|-------------|
| f0-f11 | Continuous | 12 anonymized user features |
| treatment | Binary | Randomized assignment to RTB auction (Instrument Z) |
| exposure | Binary | Whether user saw an ad (Treatment D) |
| conversion | Binary | Whether user converted (Outcome Y) |

- **Observations:** ~14 million
- **Compliance rate:** 3.6% (one-sided non-compliance)

## References

- Diemert, E., et al. (2018). "A Large Scale Benchmark for Uplift Modeling." *KDD Workshop on Causal Discovery*.

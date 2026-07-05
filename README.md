# Motor Imagery Classification: Subject-Specific Frequency Optimization

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Library](https://img.shields.io/badge/Library-MNE--Python-purple)
![Method](https://img.shields.io/badge/Method-Riemannian%20Geometry-green)
![Status](https://img.shields.io/badge/Status-Complete-success)

## Project Overview
This project builds a Brain-Computer Interface (BCI) pipeline to classify **Left vs. Right Hand Motor Imagery** from EEG data using the **BCI Competition IV 2a** dataset.

The current notebook emphasizes **evaluation rigor**:
- subject-specific band selection is done on **training data only**
- final metrics are reported on a **held-out test set**
- confusion matrices are generated from held-out predictions (not training data)

This makes the reported performance more conservative and realistic for generalization.

Dataset link: https://www.kaggle.com/datasets/thngdngvn/bci-competition-iv-data-sets-2a/data  
Note: `.mat` files are not in this repo due to size; download from Kaggle and place them in the project root.

## Methods
- **Signal stack:** MNE + SciPy
- **Feature extraction:** Covariance estimation (`pyriemann`) + Tangent Space mapping
- **Classifier:** Logistic Regression with GridSearchCV
- **Bands tested:** `7-30 Hz`, `8-35 Hz`, `12-30 Hz`, `8-14 Hz`
- **Personalization:** Per-subject frequency-band selection

## Leakage-Safe Holdout Results

| Method | Frequency Band | Mean Holdout Accuracy | Notes |
| :--- | :--- | :--- | :--- |
| Baseline | Standard (7-30 Hz) | 59.83% | Reference setup |
| Global Best | Beta (12-30 Hz) | 62.30% | Best single band across group |
| Subject-Specific | Per-subject optimized | **63.07%** | Best overall holdout performance |

### Outcome
- **+3.24 percentage points** vs baseline
- **+0.77 percentage points** vs global best single-band approach

### Subject-Level Highlights
- Beta (12-30 Hz) was selected for **6/9 subjects**
- Extended (8-35 Hz) was selected for **3/9 subjects**
- Best subject holdout accuracy: **A08T = 89.66%**
- Lowest subject holdout accuracy: **A04T = 40.00%**

## Statistical Notes
Exploratory paired tests (with Bonferroni correction) did not show statistically significant differences between single-band means at `n=9` subjects. This project should be viewed as strong evidence of a useful engineering direction, with larger studies needed for stronger inferential claims.

## Reproducibility
1. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
2. Download BCI IV 2a `.mat` files from the Kaggle link above.
3. Place dataset files in the project root.
4. Run `Motor_Imagery_Decoding.ipynb` top-to-bottom.

## Next Improvements
- Session-wise or cross-session validation (stronger external validity)
- Artifact handling with EOG/ICA
- Baseline comparisons against FBCSP / EEGNet under the same leakage-safe protocol


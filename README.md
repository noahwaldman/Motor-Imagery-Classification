# Motor Imagery Classification with Riemannian Geometry

## Overview
Decoding imagined hand movements from EEG signals using machine learning.

## Key Results
- **Average Accuracy**: 68.01%
- **Best Subject**: 88.28% (A08)
- **Method**: Riemannian geometry + Logistic Regression

## Technical Approach
1. **Preprocessing**: 7-30 Hz bandpass filter (mu/beta rhythms)
2. **Feature Extraction**: Covariance matrices + Tangent Space projection
3. **Classification**: Logistic Regression with GridSearchCV
4. **Validation**: 5-fold cross-validation

## Dataset
BCI Competition IV Dataset 2a - 9 subjects, left/right hand imagery: https://www.kaggle.com/datasets/thngdngvn/bci-competition-iv-data-sets-2a

## Technologies
- Python, MNE, scikit-learn, pyRiemann

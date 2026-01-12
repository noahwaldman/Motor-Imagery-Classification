# Motor Imagery Classification: Subject-Specific Frequency Optimization

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Library](https://img.shields.io/badge/Library-MNE--Python-purple)
![Method](https://img.shields.io/badge/Method-Riemannian%20Geometry-green)
![Status](https://img.shields.io/badge/Status-Complete-success)

## 🧠 Project Overview
This project implements a Brain-Computer Interface (BCI) pipeline to classify **Left vs. Right Hand Motor Imagery** from EEG data.

Using the **BCI Competition IV 2a dataset** (https://www.kaggle.com/datasets/thngdngvn/bci-competition-iv-data-sets-2a/data), I developed a machine learning pipeline that outperforms standard fixed-frequency approaches. By combining **Riemannian Geometry** (Covariance Matrices + Tangent Space Mapping) with a novel **Subject-Specific Frequency Optimization** step, I achieved a **72.0% average accuracy**, improving upon the standard baseline of 68%.

**Note:** The files from the dataset were too large to be uploaded to the repository, so to use the code, you need to download the files from the link above.

## 🚀 Key Features
* **Riemannian Geometry Pipeline:** Utilizes `pyriemann` to map EEG covariance matrices into the Tangent Space, providing robust features for Logistic Regression.
* **Subject-Specific Optimization:** Instead of a "one-size-fits-all" filter (e.g., 8-30 Hz), this project dynamically assigns the optimal frequency band (Mu vs. Beta) for each subject.
* **Automated Grid Search:** Systematically tests multiple frequency ranges (`7-30Hz`, `8-35Hz`, `12-30Hz`, `8-14Hz`) to maximize individual decoding performance.
* **Neurophysiological Validation:** Analyzes *why* certain subjects perform better in specific bands (e.g., "Mu-Dominant" vs. "Beta-Dominant" responders).

## 📊 Results
The optimization strategy yielded a **~4% improvement** over the standard literature baseline for this dataset.

| Method | Frequency Band | Average Accuracy | Notes |
| :--- | :--- | :--- | :--- |
| **Baseline** | Standard (7-30 Hz) | 68.01% | Typical literature setting |
| **Global Best** | Beta Focus (12-30 Hz) | 70.11% | Best single band for group |
| **My Approach** | **Subject-Specific** | **72.00%** | **Optimized per user** |

### Key Insights
* **Inter-Subject Variability:** 4/9 subjects performed best in the **Beta (12-30 Hz)** band, while others required the wider **Extended (8-35 Hz)** band.
* **The "Mu" Specialist:** Subject `A03T` achieved **80% accuracy** only when isolated to the **Mu (8-14 Hz)** rhythm, a detail lost in broader filters.
* **Rescuing Performance:** Subject `A05T` improved from **55%** (random chance) to **68%** simply by switching from a broad filter to a Beta-focused filter.


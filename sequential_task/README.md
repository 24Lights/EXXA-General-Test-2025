# Planetary Transit Detection from Light Curves

This task , we have to do the binary classification task of detecting planetary transits from light curve time series data. These transits appear as  dips in a star’s brightness when a planet passes in front of it, and identifying them is a key step in exoplanet detection.

---

## Problem Statement

The task is to classify whether a light curve contains a transit or not . The challenge lies in:

- The subtle nature of transit signals.
- Imbalanced datasets (far fewer transit examples).
- Temporal and local dependencies in the data.

---

## Approach 

### 1. Synthetic Data Generation
- Created synthetic light curves mimicking real Kepler mission observations.
- Used transit modeling with `pytransit`, and added:
  - Random noise
  - Stellar variability
  - Local shifts & stretches to simulate natural distortions.

### 2. Data Augmentation
- Augmented real Kepler data with synthetic transits.
- Applied:
  - Noise addition
  - Random phase shifts
  - Interpolation-based temporal distortions

### 3. Preprocessing
- All light curves normalized per sample to preserve transit depth information while eliminating global brightness biases.
- Used `SMOTE` to oversample minority class (transit curves) and balance the dataset.

---

## Model Architecture

### CNN + LSTM Hybrid
- 1D Convolution layers to capture local patterns and short-term dips.
- Bidirectional LSTM layers to capture sequential and temporal dependencies.

### Loss Function
- Focal Loss to address class imbalance and hard-to-classify dips. This is developed by Google.
  Ref : https://medium.com/elucidate-ai/an-introduction-to-focal-loss-b49d18cb3ded
  Ref : https://pypi.org/project/focal-loss/
- Also combined with Binary Cross-Entropy (BCE).

---

## Evaluation

- ROC-AUC, F1-score, precision-recall curves used for evaluation.
- Best threshold is chosen based on max F1-score using `precision_recall_curve`.

---

## Takeaways

- Autoencoder-based simulations help synthesize highly realistic light curves.
- SMOTE dramatically improves recall for minority transit class.
- CNN-LSTM hybrid model is effective for this type of time series + event detection task.
- Focal loss boosts performance on rare-event detection tasks like this one.

## Future scope

- Form a better synthetic data by incorporating real astrophysical noise to simulate more realistic light curves.
- Multi-class Classification: Extend the binary classification to multi-class settings for different types of transits (e.g., single-planet, binary-star etc).
- Try with Transformer architectures.
- Train representation models using unlabeled light curves to better capture variability features



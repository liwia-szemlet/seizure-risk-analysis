# Automated Seizure Detection and Risk Analysis via Multi-axis Accelerometry

This repository contains a comprehensive analytical pipeline for the automated detection of seizure events using accelerometry (ACM) signals. The project is designed according to rigorous medical signal processing standards and machine learning methodologies specifically tailored for highly imbalanced clinical datasets.

**View rendered Jupyter notebooks content here:**
* **01_data_exploration:** https://nbviewer.org/github/liwia-szemlet/seizure-risk-analysis/blob/main/notebooks/01_data_exploration.ipynb
* **02_feature_eng:** https://nbviewer.org/github/liwia-szemlet/seizure-risk-analysis/blob/main/notebooks/02_feature_eng.ipynb
* **03_model_xgboost:** https://nbviewer.org/github/liwia-szemlet/seizure-risk-analysis/blob/main/notebooks/03_model_xgboost.ipynb


## Signal Processing and Feature Engineering

The feature extraction process is based on tri-axial motion signals, processed to ensure sensor-orientation invariance and robust temporal representation.

* **Magnitude Extraction**: The Euclidean Norm (L2) of the X, Y, and Z axes was calculated to render the model independent of the physical orientation of the wearable device on the patient's limb.
* **Temporal Segmentation**: Signals were segmented using 10-second windows with a 5-second (50%) overlap to maintain temporal continuity while increasing the density of the training samples.
* **Feature Domain**: First and second-order statistics, including the mean, standard deviation, and variance of the motion magnitude, were computed for each window to capture the dynamic characteristics of seizure activity.

## Predictive Modeling and Performance Analysis

The classification utilizes the Extreme Gradient Boosting (XGBoost) algorithm. Given that seizure events represent a fraction of a percent of the total recording time (a 1:216 ratio), the loss function was optimized using the `scale_pos_weight` parameter to mitigate majority class bias.

* **Balanced Accuracy (76.11%)**: This metric, representing the arithmetic mean of sensitivity and specificity, confirms the model's ability to distinguish between classes despite the extreme asymmetry of the clinical data.
* **Recall / Sensitivity (55.00%)**: The model successfully identifies over half of the clinical seizure events based solely on motion dynamics, which is a critical threshold for clinical screening tools.
* **Specificity (98.00%)**: The high specificity rate minimizes False Positives, a vital requirement for reducing alarm fatigue in clinical monitoring environments.

## Clinical Context: Differential Analysis of Seizures and Tremors

The mathematical analysis of seizure dynamics enables the objective differentiation of involuntary movement etiologies, particularly in complex clinical settings.

* **Epilepsy**: Tonic-clonic seizures exhibit a specific evolution of frequency and amplitude, reflected in high variance values within the motion magnitude features.
* **Delirium Tremens (DT)**: Tremors associated with alcohol withdrawal syndrome typically present with higher frequency and lower amplitude compared to epileptic seizures. Accelerometry-based modeling allows for the objective separation of these states, facilitating appropriate pharmacological intervention (e.g., benzodiazepines for DT versus antiepileptic drugs for epilepsy).
* **Addiction Treatment Monitoring**: This system serves as a decision-support tool in detoxification units, enabling early intervention for withdrawal-related seizures that may otherwise be missed during intermittent manual observations.

## Data Citation and References

The SeizeIT2 dataset utilized in this project is cited as follows:

Bhagubai, M., Chatzichristos, C., Swinnen, L., Macea, J., Zhang, J., Lagae, L., Jansen, K., Schulze-Bonhage, A., Sales, F., Mahler, B., Weber, Y., Paesschen, W. V., & Vos, M. D. (2025). **SeizeIT2: Wearable Dataset Of Patients With Focal Epilepsy.** https://doi.org/10.48550/arXiv.2502.01224

**Supplemental Literature:**

1. Glaser, C. B., et al. (2022). *Distinguishing alcohol withdrawal seizures from epilepsy: A clinical and kinematic approach.* Journal of Clinical Medicine.
2. Beniczky, S., et al. (2018). *Automated seizure detection using wearable devices: A review.* Seizure: European Journal of Epilepsy.

## Project Structure

* `notebooks/`: Contains modules for preprocessing, feature engineering, and model optimization.
* `results/`: Stores confusion matrices and feature importance analyses.
* `models/`: Contains serialized model objects in JSON format.

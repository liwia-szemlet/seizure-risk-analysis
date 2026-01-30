# Accelerometry-Based Seizure Event Classification (Exploratory ML Pipeline)

This repository presents an experimental machine learning pipeline for classifying seizure-related motion patterns using wearable accelerometry data. The project focuses on feature extraction, window-based signal segmentation, and handling extreme class imbalance in biomedical time series datasets.

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

* **Balanced Accuracy (76.11%):** This metric, representing the arithmetic mean of sensitivity and specificity, confirms the model's ability to distinguish between classes despite the extreme asymmetry of the clinical data.
* **Recall (55%):** Indicates moderate sensitivity in detecting seizure-related motion patterns within this experimental dataset.
* **Specificity (98%):** Reflects strong performance in rejecting non-seizure motion segments, which is relevant for minimizing false alarms in experimental wearable-based classification tasks.

## Experimental Motion Pattern Analysis

This project explores whether motion-derived features extracted from wearable accelerometry signals can capture characteristic patterns associated with seizure activity in labeled datasets.

* The observed differences between seizure-related motion segments and other involuntary movement patterns are interpreted as statistical patterns within the dataset rather than clinically validated diagnostic distinctions.
**The pipeline is intended for research and educational purposes and does not provide medical diagnosis or treatment recommendations.**

## Limitations

- The model was trained on a retrospective dataset and has not been prospectively validated.
- Accelerometry-based detection cannot capture non-motor seizure types.
- Performance metrics reflect dataset-specific characteristics and may not generalize across wearable devices or patient populations.
- The pipeline is intended as a research prototype rather than a deployable clinical system.

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

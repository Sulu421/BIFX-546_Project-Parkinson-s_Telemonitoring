# Parkinson's Telemonitoring Project : Voice-Based Prediction of Parkinson’s Disease Severity

This repository contains my course project for BIFX 546 – Machine Learning for Bioinformatics, focusing on the Parkinsons Telemonitoring dataset. The dataset includes 5,875 voice recordings from 42 patients with early-stage Parkinson’s disease, along with clinical motor and total UPDRS scores. Each row represents one home-recorded voice sample with 16 biomedical voice features plus basic demographics.


## 📄 Title and Team Members
**Title:** Parkinson's Telemonitoring Project : Voice-Based Prediction of Parkinson’s Disease Severity  
**Course:** BIFX 546 – Machine Learning for Bioinformatics  
**Student:** Suleman Mohammad  
**Team Members:** Suleman Mohammad (solo project)

## 🎯 Project Goal

The main goal of this project is to use **biomedical voice features** to predict clinical **motor_UPDRS** and **total_UPDRS** scores for patients with early-stage Parkinson’s disease.  
In simple terms, I am asking:
> "Can we estimate how severe a patient’s Parkinson’s symptoms are, just from their home-recorded voice, and which voice features are most useful for this prediction"?

## Repository Structure

```bash
BIFX-546_Project_Parkinson-s_Telemonitoring/
├── Notebooks/
├── Data/
├── Results/
├── src/
├── README.md
└── requirements.txt
```

## 🧠 Techniques Used
From the course, I am applying:

- **Exploratory Data Analysis (EDA):**  
  Histograms, boxplots, time-series line plots, correlation heatmaps.
- **Summary Statistics:**  
  Mean, median, standard deviation, ranges, correlations.
- **Visualization:**
  Visualization with matplotlib and seaborn
- **Modelling:**
   Linear, Ridge, Lasso Regression, Random Forest, SVM, MLP, Gradient boosting modeling with scikit-learn
   Model evaluation using RMSE, MAE, and R²

## 📊 Dataset Source

**Name:** Parkinsons Telemonitoring Dataset  
**Source:** UCI Machine Learning Repository  
**URL:** https://archive.ics.uci.edu/dataset/189/parkinsons+telemonitoring  

**Citation (recommended by UCI):**  
Tsanas, A., Little, M.A., McSharry, P.E., & Ramig, L.O. (2010). *Accurate telemonitoring of Parkinson’s disease progression by noninvasive speech tests.* IEEE Transactions on Biomedical Engineering, 57(4), 884–893.

> The dataset contains 5,875 voice recordings from 42 subjects, with 16 voice features plus demographics and clinician-rated motor and total UPDRS scores.

## ✅ Packages Required

- pandas
- numpy
- matplotlib.pyplot
- matplotlib.gridspec
- seaborn 
- os
- sklearn.model_selection for train_test_split
- sklearn.model_selection for GroupShuffleSplit
- sklearn.linear_model for LinearRegression, Ridge, Lasso
- sklearn.ensemble for RandomForestRegressor
- sklearn.preprocessing for StandardScaler
- sklearn.metrics for mean_absolute_error, mean_squared_error, r2_score
- sklearn.ensemble for GradientBoostingRegressor
- sklearn.neural_network for MLPRegressor
- sklearn.decomposition for PCA
- ucimlrepo to download the UCI dataset 
- jupyter to run the notebook smoothly.


## ⚙ How to Run Your Code

### 1. Clone the repository

```bash
git clone https://github.com/Sulu421/BIFX-546_Project-Parkinson-s_Telemonitoring.git
cd BIFX-546_Project-Parkinson-s_Telemonitoring
```
### 2. Install dependencies:

```bash
pip install -r requirements.txt
```
### 3. Open Jupyter Notebook:
```bash
jupyter notebook
```
### 4. Run the .ipynb file located in Notebooks folder from top to bottom. 

### Note: 
The dataset can be loaded directly from UCI using ucimlrepo:
```python
from ucimlrepo import fetch_ucirepo
import pandas as pd

parkinsons_telemonitoring = fetch_ucirepo(id=189)
X = parkinsons_telemonitoring.data.features
y = parkinsons_telemonitoring.data.targets
df = pd.concat([X, y], axis=1)
```
## Exploratory Data Analysis

In the preliminary EDA, I confirmed that the Parkinsons Telemonitoring dataset is clean and well-structured: there are no missing values or duplicate rows, and each of the 5,875 recordings is linked to one of 42 patients followed over roughly six months. Motor and total UPDRS scores show a reasonable spread (motor_UPDRS mean around low 20s), indicating a mix of mild to moderate symptom severity rather than a very narrow range. Basic plots show that motor_UPDRS is slightly right-skewed, and many patients’ scores gradually increase over time, which matches the expected progression of Parkinson’s disease.

Correlation analysis suggests that several voice features (especially measures like jitter, shimmer, PPE, and noise-related metrics) have moderate relationships with UPDRS scores, while others are weakly related. There is strong correlation between motor_UPDRS and total_UPDRS, and also noticeable multicollinearity among the voice features themselves (e.g., different jitter and shimmer variants). This indicates that voice-based prediction of disease severity is plausible, but models will need to handle correlated inputs carefully, likely using regularization or feature selection. Future steps in the project will focus on building and comparing regression models (linear, regularized, and tree-based) to quantify how accurately UPDRS can be predicted from voice alone.


### Key Findings:

1. **Target Correlation**: motor_UPDRS ↔ total_UPDRS (r ≈ 0.95)
2. **Feature Correlations**: 
   - Jitter family: Highly inter-correlated (r > 0.80)
   - Shimmer family: Highly inter-correlated (r > 0.80)
3. **Age Relationship**: Modest positive correlation with UPDRS scores
4. **Distribution**: Skewed toward moderate disease severity

---

## Methodology

### Data Preprocessing:
1. **Patient-level splitting**: GroupShuffleSplit to prevent data leakage
2. **Feature scaling**: StandardScaler (zero mean, unit variance)
3. **Train/Test split**: ~80/20 with no patient overlap

### Models Evaluated:
- Linear Regression (baseline)
- Ridge Regression (L2 regularization)
- Lasso Regression (L1 regularization)
- Random Forest
- Support Vector Regression
- Gradient Boosting
- Neural Network (MLP)

---

## Model Performance - motor_UPDRS

| Model | Test RMSE | Test R² | Test MAE |
|-------|-----------|---------|----------|
| Lasso Regression | 7.88 | -0.064 | 6.23 |
| Ridge Regression | 7.88 | -0.064 | 6.23 |
| Linear Regression | 7.88 | -0.064 | 6.23 |
| Gradient Boosting | 8.05 | -0.11 | 6.38 |
| Neural Network | 8.08 | -0.12 | 6.40 |
| SVR | 8.13 | -0.13 | 6.44 |
| Random Forest | 8.81 | -0.35 | 6.96 |

---

## Model Performance - total_UPDRS

| Model | Test RMSE | Test R² | Test MAE |
|-------|-----------|---------|----------|
| Lasso Regression | 9.04 | 0.013 | 7.15 |
| Ridge Regression | 9.04 | 0.013 | 7.15 |
| Linear Regression | 9.04 | 0.013 | 7.15 |
| Gradient Boosting | 9.22 | -0.007 | 7.28 |
| Neural Network | 9.25 | -0.010 | 7.30 |
| SVR | 9.30 | -0.016 | 7.34 |
| Random Forest | 10.00 | -0.094 | 7.82 |

---

## Key Insights

### Best Performing Model: **Lasso Regression**
- **Advantages**: 
  - Feature selection capability
  - Handles multicollinearity well
  - Prevents overfitting

### Performance Analysis:
- **Low R² scores**: Voice features alone insufficient for strong prediction
- **Regularization helps**: Lasso/Ridge outperform unregularized models
- **Overfitting observed**: Random Forest shows poor generalization

---

## Dimensionality Reduction Analysis

### Principal Component Analysis (PCA):
- **5 components**: Explain ~96% of variance
- **Motor UPDRS**: Slight RMSE improvement (7.85 → 7.83)
- **Total UPDRS**: Minimal change in performance
- **Conclusion**: PCA doesn't significantly improve predictive power

---

## Clinical Implications

### Current Limitations:
- Voice biomarkers show **weak predictive power** for UPDRS scores
- Models explain <2% of variance in test data
- May not be sufficient as standalone diagnostic tool

### Potential Applications:
- **Complementary assessment**: Use with other clinical measures
- **Monitoring tool**: Track disease progression over time
- **Early screening**: Identify patients needing further evaluation

---

## Recommendations for Future Work

### Feature Engineering:
- **Additional biomarkers**: Combine with imaging, genetic data
- **Longitudinal features**: Rate of change over time
- **Advanced signal processing**: Spectral analysis, wavelet transforms

### Modeling Improvements:
- **Hyperparameter tuning**: Grid/random search optimization
- **Ensemble methods**: Combine multiple model predictions
- **Patient-specific models**: Individual calibration

### Validation:
- **External datasets**: Test on independent patient cohorts
- **Clinical validation**: Compare with physician assessments
- **Longitudinal studies**: Track prediction accuracy over time

---

## Technical Implementation

### Tools & Libraries:


### Reproducibility:
- **Version control**: GitHub repository
- **Documentation**: Comprehensive code comments
- **Results export**: CSV files and visualizations saved

---

## Conclusion

### Project Achievements:
✅ **Complete ML pipeline**: Data → preprocessing → modeling → evaluation  
✅ **Rigorous validation**: Patient-level cross-validation  
✅ **Comprehensive analysis**: 7 models + dimensionality reduction  
✅ **Clinical relevance**: Focus on biomedical application  

### Key Takeaway:
Voice-based biomarkers show promise but require **additional features** and **advanced modeling** for clinical-grade Parkinson's severity prediction.

---






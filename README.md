# Parkinsons Telemonitoring – BIFX 546 Project

This repository contains my course project for BIFX 546 – Machine Learning for Bioinformatics, focusing on the Parkinsons Telemonitoring dataset. The dataset includes 5,875 voice recordings from 42 patients with early-stage Parkinson’s disease, along with clinical motor and total UPDRS scores. Each row represents one home-recorded voice sample with 16 biomedical voice features plus basic demographics.


## 📄 Title and Team Members
**Title:** Voice-Based Prediction of Parkinson’s Disease Severity  
**Course:** BIFX 546 – Machine Learning for Bioinformatics  
**Student:** Suleman Mohammad  
**Team:** Solo project

## 🎯 Project Goal

The main goal of this project is to use **biomedical voice features** to predict clinical **motor_UPDRS** and **total_UPDRS** scores for patients with early-stage Parkinson’s disease.  
In simple terms, I am asking:
> "Can we estimate how severe a patient’s Parkinson’s symptoms are, just from their home-recorded voice, and which voice features are most useful for this prediction"?

## 🧠 Techniques Used
From the course, I am applying:

- **Exploratory Data Analysis (EDA):**  
  Histograms, boxplots, time-series line plots, correlation heatmaps.
- **Summary Statistics:**  
  Mean, median, standard deviation, ranges, correlations.

## 📊 Dataset Source

**Name:** Parkinsons Telemonitoring Dataset  
**Source:** UCI Machine Learning Repository  
**URL:** https://archive.ics.uci.edu/dataset/189/parkinsons+telemonitoring  

**Citation (recommended by UCI):**  
Tsanas, A., Little, M.A., McSharry, P.E., & Ramig, L.O. (2010). *Accurate telemonitoring of Parkinson’s disease progression by noninvasive speech tests.* IEEE Transactions on Biomedical Engineering, 57(4), 884–893.

> The dataset contains 5,875 voice recordings from 42 subjects, with 16 voice features plus demographics and clinician-rated motor and total UPDRS scores.

## ⚙ How to Run Your Code

### 1. Clone the repository

```bash
git clone https://github.com/Sulu421/BIFX-546_Project-Parkinson-s_Telemonitoring.git
cd BIFX-546_Project-Parkinson-s_Telemonitoring
```
## 📝 Summary of Findings

In the preliminary EDA, I confirmed that the Parkinsons Telemonitoring dataset is clean and well-structured: there are no missing values or duplicate rows, and each of the 5,875 recordings is linked to one of 42 patients followed over roughly six months. Motor and total UPDRS scores show a reasonable spread (motor_UPDRS mean around low 20s), indicating a mix of mild to moderate symptom severity rather than a very narrow range. Basic plots show that motor_UPDRS is slightly right-skewed, and many patients’ scores gradually increase over time, which matches the expected progression of Parkinson’s disease.

Correlation analysis suggests that several voice features (especially measures like jitter, shimmer, PPE, and noise-related metrics) have moderate relationships with UPDRS scores, while others are weakly related. There is strong correlation between motor_UPDRS and total_UPDRS, and also noticeable multicollinearity among the voice features themselves (e.g., different jitter and shimmer variants). This indicates that voice-based prediction of disease severity is plausible, but models will need to handle correlated inputs carefully, likely using regularization or feature selection. Future steps in the project will focus on building and comparing regression models (linear, regularized, and tree-based) to quantify how accurately UPDRS can be predicted from voice alone.














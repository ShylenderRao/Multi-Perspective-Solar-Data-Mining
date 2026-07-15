# Multi-Perspective Solar Irradiance Forecasting
Multi-model solar irradiance forecasting using K-Means, Gradient Boosting and LSTM

A data mining and machine learning project analysing 7 years of 
NSRDB (National Solar Radiation Database) solar irradiance data 
using three complementary modelling approaches: unsupervised 
clustering, supervised classification, and time-series forecasting.

## Project Overview

Solar irradiance prediction is critical for energy grid planning, 
renewable energy optimisation and weather-aware resource allocation. 
This project applies multiple machine learning techniques to 
30-minute interval solar radiation data from a single geographic 
location in Wyoming, USA (43.00°N, 110.39°W), covering 2018 to 2024.

## Models and Results

### Model 1 — K-Means Clustering (Unsupervised)

Identified two distinct solar weather regimes from daylight-only data:

| Cluster | Description | Size |
|---------|-------------|------|
| Regime A | Clear / High-Efficiency days | 22,255 (50.2%) |
| Regime B | Humid / Low-Efficiency days | 22,079 (49.8%) |

### Model 2 — Gradient Boosting Classification

Classifies solar irradiance into three categories:
Low GHI (0), Medium GHI (1), High GHI (2)

| Metric | Validation (2023) | Test (2024) |
|--------|------------------|-------------|
| Accuracy | 100% | 100% |
| F1-Score (macro) | 1.00 | 1.00 |

Key features: Solar Zenith Angle, Clearness Index, Cloud Type,
Clearsky GHI, Temperature, Relative Humidity.

### Model 3 — GHI Forecasting (Gradient Boosting Regressor)

Predicts future Global Horizontal Irradiance using lag features
and meteorological variables.

| Horizon | Split | MAE | RMSE | R² |
|---------|-------|-----|------|-----|
| H=1 (30-min ahead) | Validation | 34.24 | 80.48 | 0.917 |
| H=1 (30-min ahead) | Test | 27.84 | 63.96 | **0.954** |
| H=48 (24h ahead) | Validation | 53.20 | 112.10 | 0.839 |
| H=48 (24h ahead) | Test | 47.35 | 92.93 | **0.902** |

## Dataset

- **Source:** NSRDB (National Solar Radiation Database)
- **Location:** 43.00°N, 110.39°W — Wyoming, USA
- **Period:** 2018–2024 (7 years)
- **Frequency:** 30-minute intervals
- **Train:** 87,600 rows (2018–2022)
- **Validation:** 17,520 rows (2023)
- **Test:** 17,520 rows (2024)

Download raw data from: https://nsrdb.nrel.gov

> Note: Large processed CSV files are excluded from this repo
> due to size. Run the notebook cells in order to regenerate them
> from the raw data files in `data/raw/`.

## Project Structure
solar-irradiance-forecasting/
├── assignment.ipynb          # Main notebook (all steps)
├── requirements.txt          # Python dependencies
├── data/
│   ├── raw/                  # Original NSRDB yearly CSVs
│   └── processed/            # Cleaned + feature-engineered data
├── ghi_hist_daylight.png     # GHI distribution (daylight hours)
├── ghi_season_profile.png    # Seasonal GHI profile
├── ghi_yearly_mean.png       # Yearly mean GHI trend
└── rh_vs_clearness.png       # Humidity vs clearness index

## How to Run

```bash
# 1. Clone the repo
git clone https://github.com/ShylenderRao/solar-irradiance-forecasting.git
cd solar-irradiance-forecasting

# 2. Install dependencies
pip install -r requirements.txt

# 3. Open the notebook
jupyter notebook assignment.ipynb

# 4. Run all cells in order
# Cells 1-6:  Data loading and cleaning
# Cells 7-15: Feature engineering and EDA
# Cells 16-18: Clustering (K-Means)
# Cells 19-21: Classification (Gradient Boosting)
# Cells 22-27: Forecasting (GB Regressor + SARIMAX + LSTM)
```

## Tech Stack

| Category | Tools |
|----------|-------|
| Language | Python 3.10 |
| Data | Pandas, NumPy |
| ML Models | Scikit-learn, Gradient Boosting, K-Means |
| Statistics | StatsModels (SARIMAX) |
| Deep Learning | TensorFlow (LSTM) |
| Visualisation | Matplotlib, Seaborn |


## Author

**Shylender Rao Manpuri**
[GitHub](https://github.com/ShylenderRao)

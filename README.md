# Forecasting Lake Michigan–Huron Water Levels

This project explores whether a machine learning model can forecast the Lake Michigan–Huron level of water one to six months in advance better than a physics-based model.

We merge the 74-year public data from the National Oceanic and Atmospheric Administration (NOAA) and the Great Lakes Observing System (GLOS) into a table with monthly intervals. It then compares twelve forecast models, including a physical lake model, a snowpack model for the runoff, a physics-guided convolutional neural network, gradient boosting with fixed and with tuned settings, and a linear regression on the same inputs as gradient boosting, plus two runs given the observed weather as upper bounds, over the 44 test years. It also tests how much skill is lost when the weather data arrive one to three months late.

The full write-up is [report/report.pdf](report/report.pdf).


# Results

Root-mean-square error of the forecast level, test years 1980–2023 (lower is better):

| Model | 1 month ahead | 6 months ahead |
|---|---|---|
| Persistence | 6.73 cm | 24.81 cm |
| Seasonal climatology | 4.14 cm | 15.27 cm |
| Water balance | 3.22 cm | 14.66 cm |
| Water balance + snowpack | 3.22 cm | 14.25 cm |
| Lake model | 3.26 cm | 14.78 cm |
| Lake model + snowpack | 3.25 cm | 14.40 cm |
| Gradient boosting | 3.32 cm | 15.39 cm |
| Gradient boosting + snowpack | 3.31 cm | 15.14 cm |
| Gradient boosting, tuned | 3.42 cm | 16.09 cm |
| Linear regression (same inputs as gradient boosting) | 3.17 cm | 14.06 cm |
| Hybrid (water balance + boosting) | 3.26 cm | 14.58 cm |
| Physics-guided CNN | 3.26 cm | 14.76 cm |

A linear regression on the same inputs as gradient boosting had the lowest error at one and at four to six months, and the water-balance model with a snowpack model for the runoff at two and three months, but the two cannot be told apart. The linear regression beat gradient boosting at every horizon, and tuning gradient boosting on 1950–1979 made it worse at five and six months. No machine learning model was clearly better than the plain water-balance model.


# How to run

```
pip install -r requirements.txt
```

Run `notebooks/data_processing.ipynb`, then `notebooks/main.ipynb` from top to bottom (about 25 minutes).

The results in the report were produced with Python 3.13.16, NumPy 2.5.3, pandas 3.0.6, scikit-learn 1.9.1, SciPy 1.18.1, PyTorch 2.14.1, joblib 1.6.0 and Matplotlib 3.11.2. Other versions should run, but the gradient-boosting results can differ slightly (by a few hundredths of a centimeter) between scikit-learn versions.


# Project layout

```
data/raw/         nine raw NOAA/GLOS files (never modified)
data/processed/   merged monthly table, forecasts and result tables
notebooks/        the analysis
figures/          the eleven report figures
report/           report.tex and report.pdf, the full write-up
```
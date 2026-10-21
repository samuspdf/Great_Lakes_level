# Forecasting Lake Michigan–Huron Water Levels

This project explores whether a machine learning model can forecast the Lake Michigan–Huron level of water one to six months in advance better than a physics-based model.

We merge the 74-year public data from the National Oceanic and Atmospheric Administration (NOAA) and the Great Lakes Observing System (GLOS) into a table with monthly intervals. It then compares ten forecast models, including a physical lake model, a snowpack model for the runoff and a physics-guided convolutional neural network, plus two runs given the observed weather as upper bounds, over the 44 test years.

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
| Hybrid (water balance + boosting) | 3.26 cm | 14.58 cm |
| Physics-guided CNN | 3.26 cm | 14.76 cm |

The water-balance model with a snowpack model for the runoff is the most accurate at every horizon. No machine learning model was clearly better than the plain water-balance model.


# How to run

```
pip install -r requirements.txt
```

Run `notebooks/data_processing.ipynb`, then `notebooks/main.ipynb` from top to bottom (about 8 minutes).


# Project layout

```
data/raw/         nine raw NOAA/GLOS files (never modified)
data/processed/   merged monthly table, forecasts and result tables
notebooks/        the analysis
figures/          the ten report figures
report/           report.tex and report.pdf, the full write-up
```
# Forecasting Lake Michigan–Huron Water Levels

This project explores whether a machine learning model can forecast the Lake Michigan–Huron level of water one to six months in advance better than a physics-based model.

We merge the 74-year public data from the National Oceanic and Atmospheric Administration (NOAA) and the Great Lakes Observing System (GLOS) into a table with monthly intervals. It then compares nine forecast models, including a physical lake model, a snowpack model for the runoff and a physics-guided convolutional neural network, plus two runs given the observed weather as upper bounds, over the 44 test years.


# Project layout

data/raw/         nine raw NOAA/GLOS files (never modified)
data/processed/   merged monthly table, forecasts and result tables
notebooks/        the analysis
figures/          the six report figures
report/           report.tex, the full write-up
# pulse-oximetry-sao2-alignment

## Overview
Final project for ENG1050: Introduction to Scientific Computing. The code aligns pulse-oximeter SpO2 readings with arterial blood-gas SaO2 measurements by encounter and time. It then checks how the SpO2 − SaO2 error relates to a spectrophotometer melanin index and tests a regression-based correction.

## Methods
- `final_project_code.py`
  - Builds timestamps for pulse-oximeter samples from encounter start times (or blood-gas times) and sampling rate.
  - Interpolates SpO2 at each blood-gas time within an encounter and computes the error SpO2 − SaO2.
  - Computes the correlation between error and melanin index, fits an OLS regression of error on melanin index (statsmodels), and summarizes error by melanin quartile.
  - Applies the regression as a correction and compares original vs corrected SpO2 against SaO2.
- `aligning_raw_ppg_sao2_vals.py`
  - An alternative pipeline: computes the R ratio, (AC/DC red) / (AC/DC infrared), using red/IR proxies taken from spectrophotometer wavelengths near 660 nm and 880 nm.
  - Detects stable SpO2 plateaus, removes outliers, fits 1st- or 2nd-order calibration curves, and includes a leave-one-subject-out RMSE function.
  - **If a step fails, this file substitutes synthetic signals or R values**, so its printed outputs may not reflect real data.


## Tools
Python, pandas, NumPy, SciPy, statsmodels, scikit-learn, Matplotlib, Google Colab.

## Status
Complete.

**Data:** not included. The code expects clinical tables (`patient.csv`, `encounter.csv`, `bloodgas.csv`, `pulseoximeter.csv`, `spectrophotometer.csv`). Dataset source and terms of use: https://www.nature.com/articles/s41597-025-04870-8 

**Paths:** the Google Drive path was replaced with the placeholder `/path/to/data/`.

**Notes:** The `.py` files are exports of Google Colab notebooks. Lines starting with `!` (and the bare `pip install` line, where present) are notebook shell commands, and `drive.mount(...)` calls are Colab-only. Run the files cell by cell in a notebook, not as plain scripts.

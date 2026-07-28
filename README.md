 UK CPI Inflation Nowcasting Model
 --

A Python-based inflation nowcasting project exploring whether publicly available economic indicators can be used to estimate UK CPI inflation before the official ONS release.


Motivation
-

During my economics degree and placement at the Office for National Statistics, I've become interested in how macroeconomic data is produced, interpreted and used to inform policy decisions. After gaining experience working with Python and economic statistics, I wanted to apply these skills independently and build this simple inflation nowcasting model.

The aim of this project is to try to explore the challenges involved in predicting inflation in real time: which indicators are informative, how quickly economic shocks feed through into prices, and why inflation forecasting remains difficult even for professional forecasters.

 Project Overview
 -

This project is inspired by real-time forecasting approaches used by institutions such as the Bank of England and OBR.

The model combines publicly available UK and international economic indicators from ONS and FRED to generate monthly CPI inflation nowcasts before the official ONS release.

The current model uses an OLS regression framework with a rolling training window, allowing it to adapt to changes in inflation dynamics over time.


Key Findings
-

- Exchange rates were the strongest predictor in this model. GBP/USD movements showed the largest relationship with UK CPI inflation, highlighting the importance of exchange rate pass-through.

- Oil prices had a smaller direct effect than expected. This might reflect the fact that oil is priced in USD, meaning some of its effect is captured indirectly through exchange rate movements.

- The unemployment and inflation relationship was unstable in this sample, reflecting the difficulty of applying simple Phillips Curve relationships during periods of large economic shocks.

- Inflation relationships changed significantly after 2022. The model identifies a structural break around the Russia-Ukraine energy shock, with forecasting accuracy deteriorating during this period.

- Rolling estimation improved model performance. A 60-month rolling window increased out-of-sample R² from -0.445 to +0.222 by allowing the model to adapt to changing inflation dynamics.


## Latest Nowcast Accuracy Check

| Metric | Value |
|---|---|
| **Forecast month** | June 2026 |
| **Model prediction** | 3.57% |
| **95% interval** | [-0.78%, 7.92%] |
| **Actual June CPI (ONS, 22 July 2026)** | 2.6% |
| **Forecast error** | +0.97pp (overestimate) |
| **Previous CPI (May 2026)** | 2.80% |
| **BoE projection (Q2 2026)** | ~3.1% |

The model overestimated June CPI by 0.97pp. Notably, the BoE's own projection (~3.1%) also overestimated, suggesting the downwards surprise was driven by factors outside standard forecasting models, in particular a sharp fall in fuel prices in June 2026. The actual reading fell within the model's 95% confidence interval.

Methodology
-

**Data**

The model uses:
- UK CPI inflation
- Brent crude oil prices
- GBP/USD exchange rate
- UK wage growth
- UK unemployment
- US CPI inflation

Variables are transformed and lagged where appropriate to reflect economic transmission delays.  


**Model**
- Model: Ordinary Least Squares (OLS) regression
- Training approach: 60-month rolling estimation window
- Evaluation: Out-of-sample testing covering the post-2021 inflation surge

The purpose of the rolling window approach is to allow the model to adjust when relationships between economic variables change.


📁 Data Sources
-

The model combines UK and international macroeconomic indicators from ONS and FRED. Variables were selected based on their economic relationship with inflation and are transformed where appropriate before modelling.

| Variable | Source | Series | Frequency |
|---|---|---|---|
| UK CPI inflation | ONS | D7G7 | Monthly |
| Brent crude oil price | FRED | DCOILBRENTEU | Daily → Monthly |
| GBP/USD exchange rate | FRED | DEXUSUK | Daily → Monthly |
| UK wage growth | FRED (ONS AWE) | LCEAMN01GBM661S | Monthly |
| UK unemployment rate | FRED | LRHUTTTTGBM156S | Monthly |
| US CPI inflation | FRED | CPIAUCSL | Monthly |


🗂️ Repository Structure
-

```
uk-inflation-nowcasting/

├── data/
│   ├── raw/              # Downloaded data, untouched
│   └── processed/        # Cleaned and merged dataset

├── notebooks/
│   ├── 01_data_collection.ipynb
│   ├── 02_cleaning_merging.ipynb
│   ├── 03_exploratory_analysis.ipynb
│   ├── 04_modelling.ipynb
│   └── 05_forecasting.ipynb

├── outputs/
│   └── charts/           # Saved visualisations

├── requirements.txt
└── README.md
```


How to Run
-

1\. Clone repo: `git clone https://github.com/westonheller/uk-inflation-nowcasting`

2\. Install dependencies: `pip install -r requirements.txt`

3\. Add your FRED API key to `config.py`

4\. Download latest mm23.xlsx from ONS and place in `data/raw/`

5\. Run notebooks in order (01 → 05)


Limitations
-

This is a relatively simple forecasting model, and has several limitations: 

- Linear regression cannot capture nonlinear relationships between economic variables.
- Forecast uncertainty is high, particularly during periods of large economic shocks.
- Real-time forecasting is constrained by data publication lags.
- CPI data requires manual updating due to limitations with accessing ONS data programmatically.
- Wage data uses a FRED series based on the ONS Average Weekly Earnings dataset due to formatting challenges with the original ONS files.


Reflections
-

Building this model highlighted some of the challenges involved in real-time economic forecasting:

- Economic relationships can change significantly during periods of major shocks, such as the 2022 energy crisis.
- Simple models can provide useful insights but struggle when inflation dynamics change rapidly.
- Data availability and publication lags are important practical constraints when forecasting economic indicators.
- Even relatively simple forecasting models require careful decisions around variable selection, transformations and evaluation

Possible Extensions
-

Potential extensions could include comparing alternative forecasting approaches, incorporating additional economic indicators, and improving automation of the data pipeline.


Author
-

Weston Heller | University of Sheffield | Email: westonheller145@gmail.com | Linkedin: www.linkedin.com/in/weston-heller


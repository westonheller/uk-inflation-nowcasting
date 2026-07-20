\# 🇬🇧 UK CPI Inflation Nowcasting Model



A data pipeline and forecasting model that predicts UK CPI inflation before the official ONS release, using real-time economic indicators.



\## 📊 Project Overview

This project replicates the nowcasting workflow used by institutions like the Bank of England and OBR. It automatically pulls data from the FRED API and ONS publications to generate monthly CPI forecasts using linear regression with a rolling training window.



\## 🔍 Key Findings

\- Exchange rate pass-through (GBP/USD) dominates the model — the strongest predictor of UK inflation

\- Oil prices show a smaller direct effect than expected, likely because oil is USD-priced and its effect is partly absorbed by GBP/USD

\- Unemployment is positively correlated with CPI in this sample, contradicting the Phillips Curve — consistent with known empirical puzzles in UK data

\- The model identifies a clear structural break in 2022 caused by the Russia-Ukraine energy shock. Pre-2022 MAE is 1.15pp vs 2.48pp over the full test period — consistent with failures seen in institutional forecasting models (BoE, OBR)

\- A rolling 60-month window model improves R² from -0.445 to +0.222 by adapting to changing inflation dynamics



\## 📈 Latest Nowcast

| | |

|---|---|

| \*\*Forecast month\*\* | June 2026 |

| \*\*Point estimate\*\* | 3.57% |

| \*\*95% interval\*\* | \[-0.78%, 7.92%] |

| \*\*Previous CPI (May 2026)\*\* | 2.80% |

| \*\*BoE projection (Q2 2026)\*\* | \~3.1% |

| \*\*Official ONS release\*\* | 22 July 2026 |



\## 📁 Data Sources

| Variable | Source | Series | Frequency |

|---|---|---|---|

| UK CPI | ONS (mm23.xlsx) | D7G7 | Monthly |

| Brent Crude Oil | FRED | DCOILBRENTEU | Daily → Monthly |

| GBP/USD | FRED | DEXUSUK | Daily → Monthly |

| UK Wages | FRED | LCEAMN01GBM661S | Monthly |

| UK Unemployment | FRED | LRHUTTTTGBM156S | Monthly |

| US CPI | FRED | CPIAUCSL | Monthly |



\## 🗂️ Repository Structure

uk-inflation-nowcasting/

├── data/

│   ├── raw/          ← downloaded data, untouched

│   └── processed/    ← cleaned, merged dataset

├── notebooks/

│   ├── 01\_data\_collection.ipynb

│   ├── 02\_cleaning\_merging.ipynb

│   ├── 03\_exploratory\_analysis.ipynb

│   ├── 04\_modelling.ipynb

│   └── 05\_forecasting.ipynb

├── outputs/

│   └── charts/       ← all saved visualisations

├── requirements.txt

└── README.md



\## 🚀 How to Run

1\. Clone repo: `git clone https://github.com/yourusername/uk-inflation-nowcasting`

2\. Install dependencies: `pip install -r requirements.txt`

3\. Add your FRED API key to `config.py`

4\. Download latest mm23.xlsx from ONS and place in `data/raw/`

5\. Run notebooks in order (01 → 05)



\## 🧠 Methodology

\- \*\*Features:\*\* oil prices, GBP/USD exchange rate, UK wage growth and unemployment — all with economically motivated lags (1-3 months) to capture transmission delays

\- \*\*Model:\*\* OLS linear regression with a 60-month rolling training window to account for structural breaks

\- \*\*Evaluation:\*\* Train on 80% of data (2001-2021), test on 20% (2021-2026)



\## ⚠️ Limitations

\- Linear model cannot capture nonlinear inflation dynamics

\- Wide confidence intervals reflect genuine uncertainty in inflation forecasting

\- ONS API was unavailable during development — CPI data requires manual monthly download of mm23.xlsx

\- Wage data uses FRED mirror of ONS AWE series (LCEAMN01GBM661S) due to ONS file formatting issues



\## 👤 Author

Weston Heller | University of Sheffield Economics Student | www.linkedin.com/in/weston-heller | westonheller145@gmail.com


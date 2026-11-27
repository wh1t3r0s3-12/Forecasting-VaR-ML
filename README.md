# Forecasting Value at Risk with Machine Learning

**Group:** Raphaël POUNGAVANON, Rémi KORDEK — ESILV A4, Financial Engineering (IF4)

## Problem statement
Can a quantile-regression Machine Learning model forecast the 1-day 99 % Value at Risk
of the S&P 500 more accurately than historical simulation, the industry-standard baseline —
and does the gain come from the model or from the features?

## Data
- **S&P 500** (`^GSPC`) and **VIX** (`^VIX`), daily, January 2000 – November 2026, from Yahoo Finance (`yfinance`)
- Optional: macro-financial series from the FRED API
- Target: tomorrow's log-return r(t+1); the model forecasts its 1 % quantile

## Project structure
```
data/
  raw/            raw downloads (never modified)
  processed/      dataset.csv: cleaned data + features + target
notebooks/
  01_data_collecting.ipynb    download S&P 500 and VIX
  02_eda_processing.ipynb     data quality, EDA, feature engineering
  03_baseline.ipynb           historical simulation VaR + backtesting
  04_ml_models.ipynb          quantile regression models
  05_advanced_models.ipynb    ensemble and neural network
results/          figures and metrics
report/           final report
ai_governance/    CONTRIBUTIONS.md, PROMPT_LOG.md, AI_AUDIT.md
```

## How to run
1. Install the dependencies:
   ```bash
   pip install -r requirements.txt
   ```
2. (Optional, for FRED data) copy `.env.example` to `.env` and add your free FRED API key
   (https://fred.stlouisfed.org/docs/api/api_key.html)
3. Run the notebooks **in order** (01 → 05), from the `notebooks/` folder.
   Each notebook reads the output of the previous one.

## Methodology
- **Chronological split** (train / validation / test), no shuffling
- **Baseline:** historical simulation (250-day window)
- **Models:** linear quantile regression, gradient boosting (quantile loss), neural network
- **Evaluation:** pinball loss, violation rate, Kupiec and Christoffersen tests, Basel traffic light
- **Reproducibility:** fixed random seed, relative paths, pinned dependencies

## Results
*To be completed.*

## AI governance
Use of AI assistants is documented in `ai_governance/`.

## References

### VaR models and backtesting
- Engle, R. F., & Manganelli, S. (2001). *Value at risk models in finance* (Working Paper No. 75). European Central Bank. https://papers.ssrn.com/sol3/papers.cfm?abstract_id=356220
- Engle, R. F., & Manganelli, S. (2004) *CAViaR: Conditional Autoregressive Value at Risk by Regression Quantiles* https://pages.stern.nyu.edu/~rengle/CAVIAR.pdf
- Zhang, Y., & Nadarajah, S. (2017). A review of backtesting for value at risk. *Communications in Statistics – Theory and Methods*, 1–24. https://doi.org/10.1080/03610926.2017.1361984

### Machine learning for VaR forecasting
- Petneházi, G. (2021). Quantile convolutional neural networks for Value at Risk forecasting. *Machine Learning with Applications*, 6, 100096. https://doi.org/10.1016/j.mlwa.2021.100096
- Chronopoulos, I., Raftapostolos, A., & Kapetanios, G. (2023). Forecasting Value-at-Risk using deep neural network quantile regression. *Journal of Financial Econometrics*, 1–34. https://doi.org/10.1093/jjfinec/nbad014
- Qiu, Z., Lazar, E., & Nakata, K. (2024). VaR and ES forecasting via recurrent neural network-based stateful models. *International Review of Financial Analysis*, 92, 103102. https://doi.org/10.1016/j.irfa.2024.103102
- Vo, M. (2026). Deep quantile forecasting: Evaluating advanced neural networks for multi-horizon Value-at-Risk. *International Journal of Financial Studies*, 14, 218. https://doi.org/10.3390/ijfs14080218
- Amjad, R., Hassan, A., & Ahmed, Z. (2026). Neural and econometric forecasting of market risk: A comparative Value-at-Risk and Expected-Shortfall analysis across global equity markets. *Risks*, 14, 228. https://doi.org/10.3390/risks14100228

### Feature selection
- Cheng, X. (2024). A comprehensive study of feature selection techniques in machine learning models. *Insights in Computer, Signals and Systems*, 1(1).
Description : 
The dataset is a daily time series of the S&P 500 index (ticker ^GSPC) from January 2000 to today, about 6,700 trading days (check the S&P500.csv). For each day, we collect the Open, High, Low, Close prices and the traded Volume. From the adjusted closing price we compute daily log-returns r(t) = ln(P(t) / P(t-1)), which are the target variable of the project: the model forecasts the 1 % quantile of tomorrow's return (the 1-day 99 % VaR).

We would create others variables:  lagged returns, absolute returns, rolling volatilities (5, 20 and 60 days) and the intraday range (High − Low), which is a proxy for volatility. We also include the CBOE Volatility Index (^VIX), which measures the volatility implied by option prices and reflects market expectations of future risk.

Source : 
Data are downloaded with the open-source Python library `yfinance`, historical market data from Yahoo Finance. The data are free, publicly available and reproducible. In option, daily macro-financial series (10-year Treasury yield, credit spread) can be added from the FRED API (Federal Reserve Bank of St. Louis).

Justification of suitability:
Matches the problem : VaR is computed on portfolio returns; a major equity index is a realistic, diversified proxy of a bank's equity trading book.

Long history including several crises : the dot-com crash (2000–2002), the 2008 financial crisis, the 2011 euro debt crisis, the COVID crash (2020) and the 2022 rate shock. Extreme losses are rare (1 % of days), so a long sample with stress periods is necessary to train and backtest a tail-risk model.

Enough observations : about 6,500 days allow a chronological split (train/validation/test) while keeping at least 250 test days, which is the length required for regulatory backtesting.

Daily frequency : it matches the regulatory 1-day VaR horizon.

Comparable with the literature : the S&P 500 is the benchmark used in most VaR forecasting studies, so our results can be compared with the papers.

Data quality : prices are adjusted for dividends and splits; missing days (holidays) are naturally excluded and the few missing values will be checked and handled during preprocessing.
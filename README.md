# Short-Term Market Spillovers: S&P 500 and NASDAQ Composite (2023–2025)

## Project Overview
This project investigates the short-term lead-lag relationship between the two most prominent U.S. stock indices: the **S&P 500 (SPX)** and the **NASDAQ Composite (NAS)**. Using daily market data from January 2023 to December 2025, the study applies time-series regression to determine if same-day SPX returns provide a predictive signal for the next day's NASDAQ performance.

## Hypothesis
The core hypothesis posits that a positive daily return in the S&P 500 increases the probability of a positive return in the NASDAQ Composite on the following trading day more than random chance would suggest.

## Methodology
The study follows a rigorous econometric pipeline:
* Data Processing: Raw financial time-series data (sourced from Kaggle) was cleaned using Python (Pandas).
* Variable Transformation: To address the non-normality typical of financial returns, the dependent variable was transformed into nq_transf using a logarithmic scale:<br/>`nq_transf = NASDAQ_Return_1 > 0 ? log(1 + NASDAQ_Return_1) : (NASDAQ_Return_1 < 0 ? -log(1 - NASDAQ_Return_1) : 0).`
* Stationarity Testing: ADF and KPSS tests were conducted to confirm that both return series are stationary in levels, ensuring the regression results are not spurious.
* Econometric Modeling: An Ordinary Least Squares (OLS) Regression was performed in Gretl, incorporating market regime controls, momentum indicators (`Deviation_from_SMA`), and volatility measures (`SPX_Volatility_10D`).
* Diagnostic Testing: The model was evaluated for multicollinearity (VIF), autocorrelation (Durbin-Watson and LM tests), and heteroscedasticity.

## Key Findings
* Hypothesis Result: The main hypothesis was not supported. The coefficient for `SPX_Return` was negative (-0.0726) and statistically insignificant (p = 0.2278), suggesting no reliable linear predictive effect from SPX to the next day's NASDAQ return.
* Significant Predictors: The strongest predictors for next-day NASDAQ returns were `Deviation_from_SMA` (momentum) and `SPX_Volatility_10D` (risk environment), both of which showed high statistical significance (p < 0.001 and p = 0.0005, respectively).
Model Performance: The model explains approximately 9.6% of the variation in next-day returns (Adjusted R<sup>2</sup> = 0.0958), which is consistent with the high noise level inherent in daily financial forecasting.

## Tools Used
* Python (Pandas): Data cleaning and preprocessing.
* Gretl: Time-series analysis, stationarity testing, and OLS modeling.
* ChatGPT (GPT-4): Assisted in clarifying normality test interpretations and diagnostic visuals.

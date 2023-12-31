# cmd_forecast

## Commodity Forecasting for Trading Strategies

Author: Adam Foster

Supervisor: Marcin Chlebus

This is the repo for commodity return forecasting and its application in systematic trading strategies. It encompasses the model, input data, results, reference data and articles and any other thesis-related content. Documenting these components allows for reproducibility of results and acts as a centralised reference point for this thesis.

Commodity markets have been experiencing severe fluctuations over the past several years as a result of numerous geopolitical events and changing economic conditions. Considering the more recent moves would be useful in assessing model effectiveness. In addition, commodities is an asset class that receives less attention in the literature that other more material and liquid ones like equities, FX, rates, etc. Some analysis has been done for commodities using various GARCH models, supervised machine learning models like SVR. Most such papers end with comparative analysis across the models or new methodology for improving predictions. They also omit most of 2022 and 2023 during which there was significant volatility. There is little extension of such prediction to more practical use cases, like trading strategies.

## Tech

The models will be coded in Python.

### Running the Code

Please make sure you have all usual dependencies installed on your system. The most important ones include `python`, `pip` and `ipykernel`. If you're using _Visual Studio Code_ for development, you should be prompted to install them automatically. Next, follow this process:

1. Create the virtual environment: `python -m venv venv`
2. Enter `venv`: `source venv/bin/activate` on Linux or `venv\Scripts\activate.bat` on Windows
3. Upgrade your `pip`: `pip install --upgrade pip`
4. Install dependencies from the requirements file: `pip install -r requirements.txt`
5. Navigate to the Model directory and open the Jupyter Notebook IDE of your choice. Select the Python version from inside the `venv` you just created when prompted by `ipykernel` package. Suggested command: `python -m notebook`

## Scope

The paper will be the design, implementation and subsequent comparison of several types of forecasting models applied to a selection of systematic trading strategies focusing on energy commodity returns based on spot prices/front month contracts, specifically crude oil and natural gas.

GARCH and its variants will be used given its prevalence in financial asset forecasting. It considers the autoregressive and volatility-dependent nature of commodity returns.

Multivariate volatility and switching models may be considered.

A neural network of choice will be selected for a more topical and data-driven approach (likely LSTM). This model considers recent observations and forgets more distant ones, which is likely to work well for energy commodities that tend to experience sudden changes in price and oscillations around means.

Finally, the two-factor Gabillon model may be employed. The model constructs a term structure of commodities founded in stochastic calculus with long and short-term price factors, representing the broader increase in commodity prices in line with economic growth and structural changes, as well as sudden gluts and shortages, respectively. Cost of carry and convenience yield are included to make the spot-future differential evident.

The output of each model will consist of a bounded forecast of each commodity series and quantification of the error vs the actual series in the test set.

Contrarian and pair trading strategies will then be employed to make use of the forecasts and assessed ratios, such as Sharpe.

## Schedule

### To do

- Extend to even more GARCH variants (GJR-GARCH, TARCH)
- Extend to a more sophisticated modelling approach
- Roll the model into the test priod to obtain more accurate short-term forecasts
- Evaluate model performance comparing to test set
- Consider fallback treatment for log returns when asset prices are negative: nearby (last available) value or arithmetic return for the dates affected

### 03/12/23-17/12/23
- Further research into more sophisticated GARCH replacements
- Decided the model should continue to be rolled into the test period to obtain more accurate short-term forecasts that respond to latest asset moves to avoid long-term average convergence towards the end of the test set
- Concluded that AIC & BIC become weaker in more complex versions of the model due to adding parameters and that the ACFs sometimes come out flat due to empty results in the process

### 19/11/23-03/12/23
- Improved model specification iteratively
- Improved modularity to be able to run the model under different parameters (GARCH11, GARCH12, GARCH21, AR1-GARCH11, AR2-GARCH11, AR12-GARCH11)
- Visualised train vs prediction vs test
- Fixed test plot to cover entire test period
- Built a momentum systematic trading strategy incorporating the forecast of AR2-GARCH11: position of 1 whenever predicted return > 0, -1 otherwise, amplified by a scalar of 2 whenever predicted vol > last observed vol
- Calculated and plotted P&L for test period

### 05/11/23-19/11/23
- Debugged forecast issue
- Ran forecast on test set
- Cross-checked python mean equation and conditional variance equation outputs with equivalents in R
- Cross-checked outputs with simpler equity model
- Combined train, test and forecast data into one dataframe
- Visualised mean and conditional variance outputs

### 22/10/23-05/11/23
- Completed basic stats section: density plots, comparison vs normal distribution, JB test, Arch test, etc.
- Interpreted descriptive stats: leptokurtosis, negative skew, fat tails, arch effects
- Researched GARCH (and supporting stats) implementation in Python and relevant packages
- Split into basic 90/10 train/test split for the time being
- Implemented basic GARCH(1,1) with and without mean eq constant
- Calculated LB test, information criteria and ACFs on GARCH results
- Interpreted model stats: statistically significant coefficients, no further autocorrelation of squared standardised residuals, conditional variance eq functional form good based on ACF, mean eq functional form to be modified potentially based on ACF

### 08/10/23-22/10/23

- Described additional use case of prediction: investment strategies
- Collected reference material
- Set up git repo
- Set up core infra, ensuring reproducibility
- Stored all relevant python libraries with corresponding versions in the requirements list, ensuring reproducibility
- Centralised tickers in text file to avoid hard-coding these in code and to have an independent source file
- Collected WTI, Brent & HH time series and set up semi-automatic flow using FRED API
- Replaced monthly HH series with daily
- Removed TTF as the only frequency available was monthly
- Tested venv usability
- High level view of data
- Generated price plots
- Calculated log returns
- Performed basic data cleaning: replaced nulls throughout the series corresponding to bank holidays with the last non-null values available, removed starting null returns
- Temporarily reduced observations to a limited time period for faster data processing prior to modelling
- Initial implementation of ACFs and basic statistics

### Up to 08/10/23

- Research
- Checking data availability
- Understanding the Gabillon model
- Tweaking Gabillon - even the calibration routine - either not viable or not much added value alone
- Reconsidering focus on spot prices
- Dissociation from Gabillon and focus on spot allows to potentially expand scope of variables modelled

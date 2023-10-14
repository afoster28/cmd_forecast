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

### 08/10/23

- Collect crude oil time series
- Set up git repo
- Set up core infra, ensuring reproducibility
- Perform basic data cleaning & feature engineering
- Split into train-test
- Implement the most basic GARCH
- Describe additional use case of prediction: investment strategies

### Up to 08/10/23

- Research
- Checking data availability
- Understanding the Gabillon model
- Tweaking Gabillon - even the calibration routine - either not viable or not much added value alone
- Reconsidering focus on spot prices
- Dissociation from Gabillon and focus on spot allows to potentially expand scope of variables modelled

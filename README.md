# cmd_forecast

# Commodity Forecasting

This the repo for commodity return forecasting. It encompasses the model, input data, results, reference data and articles and any other thesis-related content. Documenting these components allows for reproducibility of results and acts as a centralised reference point for this thesis.

# Tech

The models will be coded in Python.

# Scope

The paper will be the design, implementation and subsequent comparison of several types of forecasting models applied to energy commodity returns based on spot prices/front month contracts, specifically crude oil and natural gas.

GARCH and its variants will be used given its prevalence in financial asset forecasting. It considers the autoregressive and volatility-dependent nature of commodity returns.

Multivariate volatility and switching models may be considered.

A neural network of choice will be selected for a more topical and data-driven approach (likely LSTM). This model considers recent observations and forgets more distant ones, which is likely to work well for energy commodities that tend to experience sudden changes in price and oscillations around means.

Finally, the two-factor Gabillon model may be employed. The model constructs a term structure of commodities founded in stochastic calculus with long and short-term price factors, representing the broader increase in commodity prices in line with economic growth and structural changes, as well as sudden gluts and shortages, respectively. Cost of carry and convenience yield are included to make the spot-future differential evident.

The output of each model will consist of a bounded forecast of each commodity series and quantification of the error vs the actual series in the test set.

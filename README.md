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

The paper spans the design, implementation and subsequent comparison of several types of forecasting models applied to asset prices and volatility in the context of systematic trading strategies. The focus is on commodity returns based on spot prices/front month contracts.

AR-GARCH and its variants are used given their prevalence in financial asset forecasting. They consider the autoregressive nature of commodity returns and clustering of volatility.

LSTM is also used given its recent display of strong performance, including in financial models. It is a type of RNN that contains a long-term cell state and allows for various modifications with each iteration of the neural network. This is likely to work well for energy commodities that tend to experience sudden changes in price and oscillations around means.

The output consists of price and volatility forecasts of each commodity, their application in momentum and mean-reversion trading strategies and evaluation metrics.


### _Archive_

_Multivariate volatility and switching models may be considered._

_Finally, the two-factor Gabillon model may be employed. The model constructs a term structure of commodities founded in stochastic calculus with long and short-term price factors, representing the broader increase in commodity prices in line with economic growth and structural changes, as well as sudden gluts and shortages, respectively. Cost of carry and convenience yield are included to make the spot-future differential evident._

## Schedule

### To do

- Modify AR-GARCH to produce dynamic next period forecast using a rolling window instead of a static forecast of many periods
- Run separate LSTM forecasts on asset price and volatility
- Consider fallback treatment for log returns when asset prices are negative: nearby (last available) value or arithmetic return for the dates affected

### 19/02/24-03/03/24
- Further research and brainstorming on approach and modelling technique
- Learning about LSTM
  - LSTMs maintain the chain-like structure of neural network and update layer
  - They handle long-term dependencies better due to the cell state
  - An input (sigmoid) layer is the first gate that decides how much information from the cell state should be passed through
  - A vector of candidate values is passed through to the cell state following multiplication by a sigmoid function
  - An output layer combines information from the cell state with another sigmoid function
- Findings:
  - ML solutions to time series forecasting point to RNNs, particularly LSTM
  - LSTM can be applied to numeric time series
  - Several papers on LSTM-GARCH and LSTM-AR ensemble models
  - These typically involve modifying LSTM neural network layers e.g. with GARCH forecasts
  - They focus primarily on volatility forecast in such cases
  - Mainly equity and crypto markets
  - Little practical application to actual investment decisions that would be driven by both directional and magnitude forecasts
- Proposal:
  - Already have basic framework for AR-GARCH forecast - mean equation and provides directional view (for positioning) and variance equation provides magnitude view (for leverage)
  - Modify AR-GARCH to produce dynamic next period forecast using a rolling window instead of a static forecast of many periods to a) prevent convergence to the long-term mean and conditional variance and b) make the forecast more realistic as all data leading up to an observation would be used in practice for an trading decision
  - Run separate LSTM forecasts on asset price and volatility
  - Choose commodity assets which are not frequently covered by the literature
  - Create the following combinations of price-vol forecasts
    - AR-GARCH
    - LSTM<sub>price</sub>-GARCH<sub>vol</sub>
    - AR-LSTM<sub>vol</sub>
    - LSTM<sub>price</sub>-LSTM<sub>vol</sub>
  - Evaluate in terms of at least RMSE and SR

### 18/12/23-18/02/24
- On hold

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

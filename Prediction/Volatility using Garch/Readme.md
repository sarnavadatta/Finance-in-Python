# Volatility Forecasting using GARCH Models

This notebook demonstrates how to forecast the volatility of HDFCBANK stock using GARCH (Generalized Autoregressive Conditional Heteroskedasticity) models.

## Notebook Contents

1.  **Data Loading and Preparation**:
    *   Download historical stock data for HDFCBANK.NS using the `yfinance` library.
    *   Calculate log returns and percentage returns.
    *   Compute realized volatility using a rolling 30-day standard deviation of log returns.

2.  **Exploratory Data Analysis**:
    *   Visualize the log returns to observe volatility clustering.

3.  **GARCH Model Fitting and Forecasting (Initial)**:
    *   Fit a GARCH(7,7) model to the log returns.
    *   Generate a 10-day ahead volatility forecast.
    *   Visualize the forecasted volatility.

4.  **GARCH Model Selection**:
    *   Implement a loop to find the best GARCH(p,q) order (with p and q ranging from 1 to 3) based on the Akaike Information Criterion (AIC).
    *   Print the best GARCH order and its corresponding AIC.

5.  **Rolling Volatility Forecasting**:
    *   Perform a rolling 1-day-ahead forecast for the next 30 days using the selected best GARCH model.
    *   Compare the predicted volatility with the realized volatility by plotting both on the same graph.

6.  **Feature Transform (Scaling)**:
    *   Scale the log returns using `StandardScaler`.
    *   Recompute realized volatility.
    *   Repeat the GARCH model selection process on the scaled returns.
    *   Perform rolling 1-day-ahead forecasts on the scaled returns and then unscale the predictions.
    *   Plot the realized and scaled predicted volatilities for comparison.

## Requirements

*   `yfinance`
*   `numpy`
*   `pandas`
*   `matplotlib`
*   `sklearn`
*   `arch`

You can install the required libraries using pip:

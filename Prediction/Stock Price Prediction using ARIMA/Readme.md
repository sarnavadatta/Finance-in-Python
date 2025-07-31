# Stock Price Forecasting using ARIMA/SARIMA

## Project Overview and Purpose

This project aims to forecast future stock prices using time series analysis techniques. Specifically, it focuses on predicting the closing prices of a given stock ticker (e.g., TATAMOTORS.NS) based on historical data. The core problem addressed is the inherent non-stationarity often present in financial time series data, which requires appropriate differencing techniques before applying forecasting models.

The project utilizes **ARIMA (AutoRegressive Integrated Moving Average)** and **SARIMA (Seasonal AutoRegressive Integrated Moving Average)** models to capture the temporal dependencies and patterns in the stock price data. The process involves data loading, exploratory data analysis, stationarity testing (using the Augmented Dickey-Fuller test), differencing to achieve stationarity, model order selection (using `pmdarima.auto_arima`), model fitting, and forecasting.

## Dataset Description and Source

The dataset used in this project consists of historical stock price data for **TATAMOTORS.NS**. The data spans from **2022-01-01** to **2025-06-19**.

The primary feature used for time series forecasting is the **Closing Price**. The data is sourced directly from Yahoo Finance using the `yfinance` Python library.

## Methodology and Approach

The project follows a standard time series analysis methodology to forecast stock prices:

1.  **Data Loading:** Historical stock price data for the specified ticker ("TATAMOTORS.NS") and date range ("2022-01-01" to "2025-06-19") is loaded directly from Yahoo Finance using the `yfinance` library.
2.  **Preprocessing:** The primary preprocessing step involves applying a logarithmic transformation to the 'Close' price. This is often done to stabilize the variance of the time series. The code checks for missing values, and in this case, no missing values were found in the 'Close' column after loading.
3.  **Time Series Analysis:**
    *   **Stationarity Testing:** The Augmented Dickey-Fuller (ADF) test is used to check for stationarity in the 'Close' price series. The initial test indicated non-stationarity.
    *   **Differencing:** To achieve stationarity, the first difference of the 'Close' price is calculated. An ADF test on the first difference shows strong evidence of stationarity, indicating that an integration order (d) of 1 is appropriate for the ARIMA model. The second difference was also tested but the first difference was sufficient.
    *   **ACF and PACF Analysis:** Autocorrelation Function (ACF) and Partial Autocorrelation Function (PACF) plots are generated for the differenced series to help in identifying potential orders for the AR (p) and MA (q) components of the ARIMA model.
4.  **Model Selection:** The `pmdarima.auto_arima` function is used to automatically search for the optimal non-seasonal ARIMA(p, d, q) order that minimizes the AIC (Akaike Information Criterion) based on the training data.
5.  **Model Training:** An ARIMA model with the optimal (p, d, q) order found by `auto_arima` is fitted to the training dataset.
6.  **Forecasting:**
    *   **Standard Forecast:** A standard forecast is generated for the entire test set period using the fitted ARIMA model.
    *   **Rolling Forecast:** A rolling forecast approach is also implemented. The model is initially trained on the training data, a one-step forecast is made, and then the actual observation from the test set is added to the training data (history) before the model is re-fitted for the next forecast step. This simulates a real-world scenario where new data becomes available over time.
7.  **Evaluation:** The performance of the forecasts is evaluated using the Root Mean Squared Error (RMSE). The RMSE is calculated for both the standard forecast and the rolling forecast on the original scale of the stock prices (after inverse transforming the log-transformed predictions and actual values).

## Code Structure and Usage

The code is organized sequentially within a Google Colab notebook, designed to be run cell by cell from top to bottom.

**Key Libraries Used:**

*   `yfinance`: For fetching historical stock price data.
*   `pandas`: For data manipulation and analysis.
*   `matplotlib`: For data visualization.
*   `statsmodels`: For time series analysis, including ADF tests and ARIMA modeling.
*   `pmdarima`: For automated ARIMA model order selection.
*   `numpy`: For numerical operations, particularly for the log transformation and inverse transformation.

**How to Run the Code:**

1.  Open the Google Colab notebook.
2.  Ensure you have a stable internet connection to fetch data from Yahoo Finance.
3.  Run each code cell in the notebook sequentially by clicking the "play" button on each cell or by using the keyboard shortcut `Shift + Enter`.
4.  The output of each cell, including plots and test results, will be displayed directly below the cell.

**Modifying Ticker and Date Range:**

To analyze a different stock or a different time period, you need to modify the following lines in the code cell where the data is fetched:

```python
ticker = "TATAMOTORS.NS" # Change this to your desired ticker symbol
start_date = "2022-01-01" # Change this to your desired start date (YYYY-MM-DD)
end_date = "2025-06-19" # Change this to your desired end date (YYYY-MM-DD)
```

After modifying these variables, rerun the data fetching cell and all subsequent cells to apply the analysis to the new data.


## Results and Visualizations

The analysis provided key insights into the stock price time series and the performance of the ARIMA model:

*   **Stationarity:** The initial analysis using the Augmented Dickey-Fuller (ADF) test and visual inspection of the time series plot and ACF plot showed that the original 'Close' price series was non-stationary (p-value > 0.05).
*   **Differencing:** Applying a first-order difference to the 'Close' price series resulted in a stationary time series, as indicated by a low ADF test p-value (p-value <= 0.05) and the rapidly decaying ACF plot of the differenced series. This confirmed that an integration order (d) of 1 is appropriate for the ARIMA model. The second difference also showed stationarity, but the first difference was sufficient.
*   **ACF and PACF Plots:** The ACF and PACF plots of the first-differenced series provided insights into potential AR(p) and MA(q) orders.
*   **Optimal ARIMA Order:** The `pmdarima.auto_arima` function, which automatically searches for the best ARIMA model order based on AIC, identified **ARIMA(0, 1, 0)** as the optimal non-seasonal model for this dataset. This suggests a simple random walk model on the log-transformed data.
*   **Standard Forecast Performance:** The standard forecast, which predicts the entire test set based on the initial model fit to the training data, resulted in an **RMSE of {:.2f}** on the original scale. As shown in the standard forecast plot, this forecast tends to be a flat line, reflecting the ARIMA(0,1,0) model's prediction that future changes are essentially random around the last observed value in the training set.
*   **Rolling Forecast Performance:** The rolling forecast approach, which updates the model with each new actual observation from the test set, showed significantly better performance with an **RMSE of {:.2f}** on the original scale. The rolling forecast plot visually demonstrates how this method adapts to the actual price movements, staying closer to the actual values compared to the standard forecast.

**Visualizations:**

The notebook includes several key visualizations:

*   **Closing Price Over Time Plot:** Shows the trend and fluctuations in the original stock closing prices.
*   **Original and First Difference Plots with ACF:** These plots illustrate the concept of stationarity and how differencing helps stabilize the variance and remove trends.
*   **Second Difference Plot with ACF:** Further demonstrates the effect of differencing, though the first difference was sufficient for stationarity in this case.
*   **PACF Plots of First and Second Difference:** Aid in identifying potential AR orders.
*   **Forecast vs Actual Test Set Plots (Log and Original Scale):** These plots visually compare the model's predictions (both standard and rolling) against the actual closing prices in the test set, both in the log-transformed scale used for modeling and the original price scale for interpretability. They clearly highlight the improved performance of the rolling forecast.

## Future Work and Improvements

Based on the current ARIMA model and analysis, several areas can be explored for potential improvements and further insights:

*   **Seasonal ARIMA (SARIMA):** Although the initial `auto_arima` search was limited to non-seasonal models, exploring seasonal components using SARIMA (`seasonal=True` in `auto_arima` or manually specifying seasonal orders) could capture potential seasonal patterns in the stock data that are not evident in the non-seasonal analysis.
*   **Other Time Series Models:** Investigate other advanced time series forecasting models such as GARCH models (specifically designed for modeling volatility), Prophet (developed by Facebook, particularly good with strong seasonality and trend), or even machine learning models like LSTMs (Long Short-Term Memory networks) which are well-suited for sequence data.
*   **Exogenous Variables:** Incorporate external factors that might influence stock prices. This could include:
    *   News sentiment related to the company or the market.
    *   Relevant economic indicators (e.g., interest rates, inflation, GDP growth).
    *   Prices of related or competitor stocks.
    *   Industry-specific data.
    These could be added as exogenous regressors (`exog` parameter) in the ARIMA or SARIMA models.
*   **Sophisticated Evaluation:** Employ more rigorous evaluation techniques:
    *   **Backtesting:** Implement a more comprehensive backtesting framework that simulates trading strategies based on the forecasts, including transaction costs and slippage, to get a more realistic assessment of profitability.
    *   **Alternative Metrics:** Use additional time series forecasting metrics beyond RMSE, such as Mean Absolute Error (MAE), Mean Absolute Percentage Error (MAPE), or directional accuracy.
*   **Extended Forecasting Horizon:** Evaluate the model's performance on longer forecasting horizons (e.g., weeks, months) to understand its capabilities and limitations for medium to long-term predictions. The rolling forecast approach can be adapted for multi-step predictions.
*   **Hyperparameter Tuning:** While `auto_arima` provides an initial optimal order, further fine-grained hyperparameter tuning (e.g., using grid search or random search with cross-validation) of the selected model's parameters (p, d, q, and potentially seasonal P, D, Q, M) could potentially yield better performance.
*   **Alternative Data Transformations:** Experiment with other data transformations besides the logarithmic transformation, such as Box-Cox transformations, to see if they better stabilize the variance or improve model fit.
*   **Handling Volatility:** Stock prices are known for their volatility. Explicitly modeling volatility using GARCH or similar models alongside the mean forecasting model could provide more robust predictions and confidence intervals.



## Summary:

### Data Analysis Key Findings

*   The project forecasts stock prices using ARIMA/SARIMA models, addressing the challenge of non-stationarity in financial time series data.
*   The dataset used is historical closing price data for TATAMOTORS.NS from 2022-01-01 to 2025-06-19, sourced via the `yfinance` library.
*   The methodology includes data loading, logarithmic transformation for preprocessing, stationarity testing (ADF test), differencing (first difference was sufficient), ACF/PACF analysis, automated model selection using `pmdarima.auto_arima`, model training, and both standard and rolling forecasts.
*   Forecast evaluation is performed using Root Mean Squared Error (RMSE) on the original scale of the stock prices.
*   The code is structured sequentially in a Google Colab notebook, using libraries like `yfinance`, `pandas`, `matplotlib`, `statsmodels`, `pmdarima`, and `numpy`. Instructions are provided on how to run the code and modify the ticker and date range.
*   The analysis found the original 'Close' price series to be non-stationary, which was resolved by first-order differencing.
*   `pmdarima.auto_arima` identified ARIMA(0, 1, 0) as the optimal non-seasonal model.
*   The standard forecast resulted in an RMSE of 109.39 on the original scale, appearing as a flat line due to the ARIMA(0,1,0) model.
*   The rolling forecast significantly outperformed the standard forecast with an RMSE of 14.82 on the original scale, demonstrating better adaptation to actual price movements.
*   Visualizations in the notebook include plots of the closing price, differenced series with ACF/PACF, and forecast vs. actual comparisons.

### Insights or Next Steps

*   The rolling forecast approach is crucial for achieving better predictive performance in dynamic stock price forecasting compared to a static standard forecast.
*   Future work should explore incorporating seasonal components (SARIMA), testing other time series or machine learning models (GARCH, Prophet, LSTMs), including exogenous variables (economic indicators, news sentiment), and implementing more robust evaluation techniques like backtesting to improve the model and assess its real-world applicability.

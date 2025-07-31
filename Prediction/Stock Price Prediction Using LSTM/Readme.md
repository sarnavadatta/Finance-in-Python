# Stock Price Prediction using LSTM

## Project Overview and Purpose

This project aims to predict the future closing prices of a stock (HDFCBANK.NS) using a Long Short-Term Memory (LSTM) neural network. The purpose is to build a time series forecasting model that can capture complex patterns and dependencies in historical stock data, including technical indicators and volume, to make informed predictions.

## Dataset Description and Source

The dataset used in this project consists of historical stock price data for **HDFCBANK.NS**, fetched directly from Yahoo Finance using the `yfinance` library. The data spans from January 1, 2018, to June 30, 2025, and includes the following columns:

- **Open:** The opening price of the stock for the day.
- **High:** The highest price of the stock for the day.
- **Low:** The lowest price of the stock for the day.
- **Close:** The closing price of the stock for the day.
- **Volume:** The number of shares traded for the day.

## Methodology and Approach

The project follows a standard machine learning workflow for time series forecasting:

1.  **Data Loading:** Historical stock data is downloaded using `yfinance`.
2.  **Data Preprocessing:**
    *   Rows with zero volume are removed.
    *   A log transformation is applied to the 'Volume' column to stabilize variance.
3.  **Feature Engineering:** Several technical indicators are calculated and added as new features:
    *   Moving Averages (MA12, MA26, MA50, MA200)
    *   Relative Strength Index (RSI)
    *   Moving Average Convergence Divergence (MACD)
    *   Rows with NaN values introduced by calculating moving averages are dropped.
4.  **Feature Selection:** The 'Open', 'High', 'Low', 'Close', 'Log Volume', and all calculated technical indicators are selected as features for the model.
5.  **Data Scaling:** The selected features are scaled using `StandardScaler` to normalize the data and improve model performance.
6.  **Sequence Creation:** The data is transformed into sequences using a sliding window approach, creating input sequences (X) and corresponding target values (y) for the LSTM model. A time step of 60 is used for the first model and 30 for the second.
7.  **Train-Test Split:** The data is split into training and testing sets. The last 30 data points are reserved for testing.
8.  **Model Building:** An LSTM model is built using the Keras Sequential API. The model consists of multiple LSTM layers with Dropout for regularization and a final Dense layer for output. Two different models are built and evaluated: one using multiple features and another using only the 'Close' price.
9.  **Model Compilation:** The model is compiled with the 'adam' optimizer and 'mean\_squared\_error' as the loss function. The first model also includes 'RootMeanSquaredError' as a metric.
10. **Model Training:** The model is trained on the training data with a specified number of epochs and batch size. Early stopping is implemented for the first model to prevent overfitting.
11. **Prediction:** The trained model is used to make predictions on the test set.
12. **Inverse Scaling:** The predicted and actual prices are inverse-scaled to return them to their original price range.
13. **Evaluation:** Performance metrics (Mean Absolute Error (MAE) and Root Mean Squared Error (RMSE)) are calculated to assess the model's accuracy.
14. **Visualization:** The actual and predicted closing prices are plotted to visually compare the model's performance.

## Code Structure and Usage

The code is organized into sequential cells within the Google Colab notebook. Each cell performs a specific step in the data science workflow, from data loading to model evaluation and visualization.

To use the notebook:

1.  Open the notebook in Google Colab.
2.  Run each cell sequentially.
3.  Ensure all necessary libraries are installed (they are typically pre-installed in Colab or installed in the first code cell).
4.  Modify the `ticker`, `start_date`, and `end_date` variables in the data loading cell to analyze different stocks and time periods.
5.  Experiment with different time steps, model architectures, and hyperparameters to potentially improve results.

## Results and Visualizations

The project provides MAE and RMSE metrics to quantify the model's performance on the test set. Additionally, a plot is generated comparing the actual and predicted closing prices, allowing for a visual assessment of how well the model tracks the stock's movement.

*   **Model 1 (Multiple Features):**
    *   MAE: 16.68
    *   RMSE: 24.36
*   **Model 2 (Close Price - Only):**
    *   MAE: 33.43
    *   RMSE: 39.26

The plots show how closely the predicted prices follow the actual prices, providing a visual representation of the model's accuracy.

## Future Work and Improvements

Possible future improvements include:

*   **Hyperparameter Tuning:** Optimize the LSTM model's hyperparameters (e.g., number of units, layers, dropout rates, learning rate) using techniques like GridSearchCV or RandomizedSearchCV.
*   **More Advanced Technical Indicators:** Incorporate a wider range of technical indicators (e.g., Bollinger Bands, Moving Average Convergence Divergence (MACD) Signal Line, Stochastic Oscillator) to potentially provide more predictive power.
*   **Alternative Models:** Explore other time series forecasting models like GRU, ARIMA, or Prophet to compare their performance against the LSTM model.
*   **Sentiment Analysis:** Integrate sentiment data from news articles or social media to capture market sentiment, which can influence stock prices.
*   **Economic Factors:** Consider incorporating macroeconomic indicators (e.g., interest rates, inflation) that might impact stock market trends.
*   **Walk-Forward Validation:** Implement a more robust evaluation strategy like walk-forward validation to simulate real-world trading scenarios.
*   **Ensemble Methods:** Experiment with ensemble methods that combine predictions from multiple models to potentially improve accuracy and robustness.
*   **GPU Acceleration:** Ensure the model training leverages GPU acceleration in Colab for faster training times, especially with larger datasets or more complex models.

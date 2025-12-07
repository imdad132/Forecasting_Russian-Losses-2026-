
# Russian Losses Forecasting: 2026 Scenario Analysis

### A Machine Learning & Time-Series approach to analyzing the Russo-Ukrainian War

## 📌 Overview

This project analyzes historical data of Russian military losses in the Ukraine war (2022–Present) to identify trends, correlations, and forecast potential personnel losses for the year 2026.

Unlike simple linear projections, this project employs a **"Link Model" methodology**: it first establishes the statistical relationship between equipment losses (Tanks, APCs, Artillery) and personnel casualties, and then forecasts future personnel losses based on three distinct equipment attrition scenarios.

## 📊 Key Findings & Methodology

### 1\. Data Preprocessing

The raw data is cumulative. The script performs the following transformations:

  * **Cumulative to Daily:** Converts running totals into daily incremental losses using `df.diff()`.
  * **Anomaly Detection:** Filters out data correction artifacts (negative values) to ensure data integrity.
  * **Smoothing:** Applies a 30-day rolling average to visualize tactical phases of the war (high-intensity offensives vs. positional lulls).

### 2\. Correlation Analysis

The project investigates the tactical relationship between different loss categories.

  * *Heatmap Visualization:* Determines how strongly personnel losses correlate with heavy equipment losses (Tanks, Artillery) versus asymmetric assets (Drones).

### 3\. The "Link Model" Approach

Instead of forecasting personnel losses in isolation, we train a **Linear Regression** model to predict `Daily Personnel Losses` based on `Daily Equipment Losses`.

  * **Hypothesis:** High equipment loss days (mechanized assaults) are strong predictors of high personnel attrition.

### 4\. 2026 Forecasting Scenarios

The model projects personnel losses for 2026 based on three different futures for equipment attrition:

  * **Scenario A: Status Quo (Baseline)**
      * *Method:* Projects the average equipment losses of the **last 90 days** forward.
      * *Assumption:* The conflict intensity remains exactly as it is currently.
  * **Scenario B: Linear Trend**
      * *Method:* Uses Linear Regression to project the long-term trajectory of equipment losses.
      * *Assumption:* Recent trends (e.g., depletion of vehicle stocks) continue linearly.
  * **Scenario C: ARIMA Cycles**
      * *Method:* Uses **ARIMA (AutoRegressive Integrated Moving Average)** to forecast equipment losses.
      * *Assumption:* Historical patterns and cyclical volatility will repeat.

## 🛠️ Tech Stack

  * **Python 3.x**
  * **Pandas & NumPy:** Data manipulation and time-series handling.
  * **Scikit-Learn:** Linear Regression for the "Link Model."
  * **Statsmodels:** ARIMA modeling for time-series forecasting.
  * **Plotly:** Interactive visualization for scenario comparison.
  * **Seaborn/Matplotlib:** Exploratory Data Analysis (EDA) and heatmaps.

## 🚀 Installation & Usage

1.  **Clone the repository:**

    ```bash
    git clone https://github.com/your-username/russian-losses-forecast.git
    cd russian-losses-forecast
    ```

2.  **Install dependencies:**

    ```bash
    pip install pandas numpy matplotlib seaborn plotly scikit-learn statsmodels nbformat
    ```

3.  **Add the Data:**
    Ensure `russian_losses.csv` is in the root directory. (Data source: [Kaggle](https://www.kaggle.com/datasets/piterfm/2022-ukraine-russian-war))

4.  **Run the analysis:**

    ```bash
    python analysis.py
    ```

## 📈 Visualizations

The script generates three key visualizations:

1.  **Daily Trends:** A scatter plot of daily losses overlaid with a 30-day rolling average trend line.
2.  **Correlation Heatmap:** A matrix showing the statistical relationship between personnel, tanks, APCs, and artillery.
3.  **2026 Forecast:** An interactive Plotly line chart comparing the three scenarios (Status Quo, Linear, ARIMA) with monthly aggregated totals.

## ⚠️ Disclaimer

  * **Data Source:** This analysis relies on data provided by the General Staff of the Armed Forces of Ukraine.
  * **Fog of War:** Conflict data is inherently subject to estimation errors, reporting lags, and the "fog of war." These forecasts are statistical projections based on reported historical patterns, not military intelligence predictions.


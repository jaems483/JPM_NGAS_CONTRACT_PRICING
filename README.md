# NGAS Price Contract Forecasting and Valuation

## Overview

This notebook explores natural gas price forecasting and contract valuation using:

- **Simple Linear Regression** for trend estimation
- **SARIMA (Seasonal ARIMA)** for time-series forecasting
- A custom **natural gas storage contract pricing model**

The workflow demonstrates how historical natural gas prices can be used to:

1. Fit predictive models
2. Forecast future prices
3. Simulate storage contract profitability under operational constraints and fees

---

## Project Structure

### Data Preparation

The notebook loads historical natural gas price data from:

```text
Nat_Gas.csv
```

The dataset is expected to contain:

| Column | Description |
|---|---|
| `Dates` | Historical observation dates |
| `Prices` | Natural gas prices |

The `Dates` column is parsed as a datetime index, and a derived `Days` feature is created for regression modeling.

---

## Modeling Approaches

### 1. Simple Linear Regression

A linear regression model is trained using:

- **Feature:** Number of days since the first observation
- **Target:** Natural gas prices

The notebook:

- Fits the regression model
- Generates historical predictions
- Visualizes:
  - Actual prices
  - Regression trend line

This section provides a baseline understanding of long-term price movement.

---

### 2. Future Price Projection

The notebook generates future monthly dates and predicts prices for the next 12 months using the trained regression model.

Outputs include:

- Forecasted monthly prices
- Visualization of:
  - Historical prices
  - Regression fit
  - Future projections

An additional prediction is calculated exactly one year after the latest available date.

---

### 3. SARIMA Forecasting

To capture seasonality and time-series dynamics more effectively, the notebook applies a **SARIMA model** using `statsmodels`.

This section:

- Prepares the time series
- Fits a SARIMA model
- Produces future price forecasts
- Extracts forecast dates and predicted values

SARIMA is more suitable than simple linear regression for cyclical commodity pricing behavior.

---

## Contract Valuation Model

The notebook includes a custom function:

```python
price_contract(...)
```

This function estimates the value of a natural gas storage contract using:

- Injection dates and prices
- Withdrawal dates and prices
- Storage capacity limits
- Injection/withdrawal rates
- Storage costs
- Transaction fees

### Inputs

| Parameter | Description |
|---|---|
| `in_dates` | Injection dates |
| `in_prices` | Prices during injection |
| `out_dates` | Withdrawal dates |
| `out_prices` | Prices during withdrawal |
| `rate` | Injection/withdrawal volume rate |
| `storage_cost_rate` | Storage fee |
| `total_vol` | Maximum storage volume |
| `injection_withdrawal_cost_rate` | Operational fee |

### Output

The function computes:

- Purchase costs
- Revenue from withdrawals
- Storage expenses
- Net contract value

---

## SARIMA-Based Contract Simulation

The notebook then uses SARIMA forecasted prices to simulate a hypothetical storage contract.

Selected forecast dates are used as:

- Injection opportunities
- Withdrawal opportunities

The resulting contract valuation demonstrates how forecast quality directly impacts profitability.

---

## Key Insight

The notebook notes that:

> Negative profitability can still occur even when withdrawal prices exceed injection prices due to operational fees and insufficient price spreads.

This highlights an important real-world consideration in commodity storage trading:

- Price direction alone does not guarantee profitability
- Storage and transaction costs significantly affect outcomes

The notebook also observes that small changes in forecasted prices can produce large differences in profitability.

---

## Dependencies

Install the required Python libraries before running the notebook:

```bash
pip install pandas numpy matplotlib scikit-learn statsmodels
```

---

## Example Workflow

1. Load historical gas price data
2. Fit a linear regression model
3. Forecast future prices
4. Fit a SARIMA model
5. Generate time-series forecasts
6. Simulate a storage contract
7. Analyze profitability

---

## Visualizations

The notebook generates several plots, including:

- Historical natural gas prices
- Linear regression fit
- Future price projections
- Forecast comparison visuals

---

## Potential Improvements

Possible enhancements for the project include:

- Hyperparameter tuning for SARIMA
- Cross-validation of forecasts
- Monte Carlo simulations
- Integration with real-time market data
- Advanced storage optimization strategies
- Comparison against Prophet or LSTM models

---

## Use Cases

This notebook can be useful for:

- Commodity trading analysis
- Energy market forecasting
- Quantitative finance projects
- Time-series modeling practice
- Storage contract valuation studies

---

## Notes

- Ensure `Nat_Gas.csv` exists in the same working directory as the notebook.
- The notebook assumes monthly frequency data.
- Forecast quality heavily influences contract valuation accuracy.


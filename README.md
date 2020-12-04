# Japanese Yen Futures

![Yen Photo](Images/adobe_stock.jpg)

## Background

I tested the various time-series tools that I have learned in order to predict future movements in the value of the Japanese yen versus the U.S. dollar.

This task is broken down into two steps:
1. Time Series Forecasting
2. Linear Regression Modeling

### Time-Series Forecasting

In this notebook, I apply time series analysis and modeling to determine whether there is any predictable behavior in Dollar-Yen exchange rate data. 


* There is an obvious long-term bullish trend in the Settle price of the historical daily Yen futures data. I see a continuation pattern forming, with price consolidating into a tighter range between 1992 to 2008 forming a symmetrical triangle followed by a price surge and consolidating again in the direction of the trend.

* I decomposed the Settle price into a trend and noise using a Hodrick-Prescott Filter.

* Using futures Settle returns, I estimated an ARMA model with the parameters p=2 and q=1: order=(2, 1).
    * Based on the p-values, the ARMA model is not a good fit because the significance level 𝜶 is .05 (5%) and the p-values are higher (p > 𝜶), therefore the relationship between the variables is not statistically significant and we cannot dismiss the null hypothesis.


* Using the raw Yen Settle Price, I estimated an ARIMA model (order=(5, 1, 1)) and based on the summary results p-values are higher than 0.05 (p > 𝜶), which also indicates that the relationship between the variables are not statistically significant and we cannot dismiss the null hypothesis.

    * The model forecasts the Japanese Yen futures settle price to increase over the 5 day forecast horizon.
    
* I created a GARCH model to forecast near-term volatility of Japanese Yen futures returns. Based on the summary table, the model seems to be a good fit (p < 𝜶).

#### Conclusions

1. Based on your time series analysis, would you buy the yen now?

   *Based on this time series analysis, I'm expecting that Yen will appreciate againt the dollar in the long-term. However, considering the near-term volatility of the currency pair and unreliable ARMA and ARIMA  forecasts, I would not feel confident in trading short-term. A longer investment time horizon would be a safer decision for now, until I find a more reliable forecasting model.*

2. Is the risk of the yen expected to increase or decrease?

   *Near-term volatility of the Japanese Yen futures returns is expected to increase based on the GARCH model, which indicates increasing risk of the Yen and/or a potential financial loss.*

3. Based on the model evaluation, would you feel confident in using these models for trading?

   *The ARMA and ARIMA models are not reliable to use for trading because the p-values are higher than 0.05 (> 0.05) which is not statistically significant and we cannot dismiss the null hypothesis. Therefore, I would not feel confident in basing my trading decisions on just these models.*


### Linear Regression Modeling

In this notebook, I built a Scikit-Learn linear regression model to predict Yen futures ("settle") returns with *lagged* Yen futures returns and categorical calendar seasonal effects.

* Created a series using Returns *(Dependent variables)* and Lagged Returns *(Independent variables)* and split the data into training and testing data.
* Fitted a Linear Regression model.
* Made predictions of returns using just the testing data.
* Evaluated the model using out-of-sample data and in-sample data separately.

#### Conclusions
1. Does this model perform better or worse on out-of-sample data compared to in-sample data?

    *The out-of-sample RMSE is lower than the in-sample RMSE. RMSE is typically lower for training data but is higher in this case. Therefore, this model performs better on out-of-sample data compared to in-sample data*

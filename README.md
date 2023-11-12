# The-Study-of-US-Mortgage-Rates

# Abstract

This project delves into the intricacies of U.S. 30-year mortgage rates (M30Y), aiming to discern causal relationships, identify cointegration patterns, and unveil robust correlations. The culmination of this research involves constructing a predictive model for weekly M30Y estimates.

In 2023, homeowners find themselves navigating the real estate market sidelines, impacted by interest rates at unprecedented levels over the past two decades. While some regions, like California and Washington, witness price pullbacks of 10%, others face challenges entering the market due to sustained prices driven by low inventory. With interest rates either rising or remaining elevated, an increasing number of homeowners closely monitor the fluctuations of the M30Y.

The project employs a series of hypothesis tests, data analysis techniques, and time series forecasting to uncover significant relationships and decipher the primary influencers behind M30Y dynamics.

Macroeconomic events, the intricacies of the financial system, and the strategies of fiscal policies unsurprisingly exert substantial influence on M30Y. The drivers of M30Y exhibit shifts based on the economic landscape—whether building up to, in the midst of, or recovering from a recession. Moreover, M30Y characteristics during the 80s and 90s appear to differ from those observed during the Global Financial Crisis (GFC) and the COVID-19 pandemic.

Yield spreads, including those between Treasury yields, Aaa and Baa government bonds, and the Fed Funds rate, emerge as crucial drivers of M30Y. Specifically, the Aaa – Treasury 10Y spread demonstrates causal properties influencing the weekly returns of M30Y.

The study unravels a strong seasonal pattern within the M30Y data, identifying a significant two-year cycle (52*2 weeks) with statistical significance beyond the 1% threshold.

# Introduction

Please use the Table of Contents, found below, to navigate the project!

In this project I extract the following series using the FRED API:
-	MORTGAGE30US, WGS10YR, WGS2YR, FF, WAAA, WBAA
The spreads between the Treasury rates, Fed Funds, and Aaa and Baa rates were calculated by subtraction.

The following are independent variables in the study:
-	Treasury 10Y (T10Y), Treasury 2Y (T2Y), Federal Funds (FED), Aaa Yield (AAA), Baa Yield (BAA), Treasury 10-2Y (T10-2), Treasury 10Y-Federal Funds (T10-F), Aaa-Baa (A-B), Aaa-Treasury 10Y (A-T10)

The project concludes with a series of machine learning applications predicting stationary data through SARIMAX and Random Forest Regressor and ends with non-stationary prediction with Random Forest Regressor and LSTM Deep Learning.

# Table of Contents

-	Data Preparation and Cleaning: Methods behind extracting, cleaning, and transforming the data.
-	Statistical and Data Analysis: A series of 10 hypothesis tests surrounding correlation, cointegration, and volatility.
-	Machine Learning: Stationary and non-stationary forecasting.
-	Forward Testing: Forward testing with five weeks of unseen data.
-	Exhibits: A folder of figures.

# Observations and Findings

Hypothesis Test 1.1: There is no difference between the correlation using the Aaa-10Y Treasury from 50Wks ago with this week's 30Yr Mortgage and using the Aaa-10Y Treasury from 2Wks ago with this week's 30Yr Mortgage (Fisher’s Z Transformation).
-	50Wks Correlation: -.714, 2Wks Correlation: -.689, P-value: .083
-	See figure 0.

Hypothesis Test 1.2: There are no differences between the correlations all independent variables with 30Yr Mortgage rates during the recent recoveries (COVID, GFC, Dot-Com) and the historical recoveries (80s Recession, Gulf War) (Fisher’s Z Transformation).
-	1.2.1: All independent variables except for the FED and T10-F had a statistically significant difference between their correlations with M30Y during the COVID Recovery and during the 80s Recovery (See figure 1).
-	1.2.2: All independent variables except for the A-T10 and T10-F had a statistically significant difference between their correlations with M30Y during the COVID Recovery and during the Gulf War Recovery (See figure 2).
-	1.2.3: All independent variables except for the T2Y, AAA, BAA, A-B, and A-T10 had a statistically significant difference between their correlations with M30Y during the GFC Recovery and during the 80s Recovery (See figure 3).
-	1.2.4: All independent variables except for T2Y, FED, AAA, BAA, and A-B had a statistically significant difference between their correlations with M30Y during the GFC Recovery and during the Gulf War Recovery (See figure 4).
-	1.2.5: All independent variables except for the AAA had a statistically significant difference between their correlations with M30Y during the Dot-Com Recovery and during the 80s Recovery (See figure 5).
-	1.2.7: All independent variables except for T2Y, FED, AAA, BAA, and A-B had a statistically significant difference between their correlations with M30Y during the Dot-Com Recovery and during the Gulf War Recovery (See figure 6).
-	Overall 1.2: See figure 7.


Hypothesis Test 1.3: There are no differences between the correlations of yield spreads with 30Yr Mortgage rates during the two-year period leading up to a recession (Pre-GFC, Pre-Dot-Com) and the periods of recessions (GFC, Dot-Com). (Fisher’s Z Transformation).
-	1.3.1: All yield curves had a statistically significant difference between their correlations with M30Y during the two-year period leading up to the GFC and during the GFC (See figure 8).
-	1.3.2: All yield curves except for A-B had a statistically significant difference between their correlations with M30Y during the two-year period leading up to the Dot-Com and during the Dot-Com (See figure 9).
-	Overall 1.3: See figure 10.

Hypothesis Test 1.4: There are no differences between the correlations of yield spreads with 30Yr Mortgage rates during the two-year period leading up to a recession (Pre-GFC, Pre-Dot-Com) and the recoveries of recessions (GFC Recovery, Dot-Com Recovery). (Fisher’s Z Transformation).
-	1.4.1: All yield curves except A-T10 had a statistically significant difference between their correlations with M30Y during the two-year period leading up to the Dot-Com and the Dot-Com recovery (See figure 11).
-	1.4.2: All yield curves had a statistically significant difference between their correlations with M30Y during the two-year period leading up to the GFC and during the GFC Recovery (See figure 12).
-	Overall 1.4: See figure 13.


Hypothesis Test 2.1: All independent variables are not stationary and contain a unit root (ADFuller).
-	T10-2, T10-F, A-B, and A-T10 are all stationary and do not contain a unit root.
-	P-values: .0008, .003, .0002, .01
-	See figure 14.

Hypothesis Test 2.2: All differenced independent variables are not stationary and contain a unit root (ADFuller).
-	All differenced independent variables had a P-value of ~0.
-	See figure 15.

Hypothesis Test 2.3: There is no cointegration between M30Y differenced and the stationary independent variables (differenced rates and non-differenced yield spreads) (Engle-Granger two-step cointegration test).
-	All stationary variables are cointegrated with M30Y differenced, P-Value: ~0.
-	See figure 16.

VIF Testing for multicollinearity:
-	Using 10 as the cutoff, T10-2, T10-F, and A-B are scored high on the multicollinearity VIF test.
-	See figure 17.

Hypothesis Test 2.4: A-T10 and differenced FED does not Granger-cause M30Y differenced.
-	2.4.1: Selected order of 7 by lowest AIC, the Johansen cointegration test showed significant cointegration between the A-T10 and the M30Y differenced, and the granger causality test had a P-Value: ~0, see figure 18.
-	2.4.2: Selected order of 9 by lowest AIC, the Johansen cointegration test showed significant cointegration between the differenced FED and the M30Y differenced, and the granger causality test had a P-Value: ~0, see figure 19.

Hypothesis Test 3.1: GARCH effects are not important in explaining volatility in the selected time series.
-	3.1.1: Alpha 1 (short term) and Beta 1 (long term) are statistically significant and play a role in explaining volatility of the differenced M30Y, see figure 20.
-	 3.1.2: Alpha 1 (short term) is statistically significant and plays a role in explaining volatility of the non-differenced A-T10, see figure 21.

Time Series Decomposition:
-	Seasonal Period of two years (52*2) resulted in random appearing residuals plot, see figure 22.

Hypothesis Test 4.1: The residuals from the Seasonal Period of two years follow a normal distribution.
-	Statistic of 28.6 with critical values of 1.09 for 1% significance.

# Model Evaluation

All machine learning models were set with the following parameters:
-	Output variable: Next week’s M30Y
-	Input variables: This week’s data points
-	Test size: 20%, shuffle = False

# Stationary Modeling

Due to importance of multicollinearity in stationary modeling, features that scored higher than 10 on the VIF test were dropped (T10-2, T10-F, and A-B, see figure 17).

Input variables: 
-	Differenced M30Y, T10Y, T2Y, FED, AAA, BAA
-	Non-differenced A-T10

SARIMAX
-	Grid search obtained the optimal P, D, Q parameters: 1, 0, 1 and M was set to 104 (two years, 52*2).
-	Poor performance MSE: 0.0096, RMSE: 0.098, MAE: 0.066768

Random Forest
-	N_estimators = 500, max_depth = 5
-	Poor performance: MSE: 0.00661, RMSE: 0.0813, MAE: 0.05398

# Non-stationary Modeling
Input variables:
-	Non-differenced independent variables

Random Forest
-	N_estimators = 50, max_depth = 5
-	Very good performance: MSE: 0.25763, RMSE: 0.5075793, MAE: 0.42292

LSTM Deep Learning
-	Window for observations = 11, two hidden layers (LSTM 32, Dense ‘relu’ 16), Adam optimizer with a learning rate of .001, 50 epochs, early stopping patience = 10
-	Excellent performance: MSE: 0.02622, RMSE: 0.161951, MAE: 0.12432

# Forward Testing Non-Stationary Models

5 weeks of new data

Random Forest
-	MSE: 0.759, RMSE: 0.8712, MAE: 0.8697
-	Predictions were adequate, with a Relative RMSE of 11.4%.

LSTM
-	MSE: 0.08275, RMSE: 0.2876, MAE: 0.28486
-	Predictions were good, with a Relative RMSE of 3.8%.


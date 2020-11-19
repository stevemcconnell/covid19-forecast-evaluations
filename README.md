# Covid19 Forecast Evaluations

Evaluations of forecasts that have been submitted in support of the CDC's Ensemble model for Covid-19 death forecasts.

Unless otherwise noted, all "errors" in the files refer to "log difference", which is calculated as ln(actual/forecast) -- which mathematically is the same as ln(actual) - ln(forecast), which is why it's called log difference. 

Only incremental forecasts are scored. 

Within a forecast set for a particular forecast date, the incremental error numbers are all cumulative for the forecast date, meaning the Forecasts for Week 2 are the incremental forecasts for Wk1+Wk2, and the actuals are also Wk1+Wk2, etc.

# Columns

Here’s a description of the csv file contents, by column header:
 
model – The CDC model name
 
forecast_date – The CDC forecast date for the summary files in M/D/YYYY format
 
target - The CDC target period, i.e., 1 wk ahead inc death, 2 wk ahead inc death, etc. Only incremental targets are contained in these files. 

target_week_end  – The CDC target week end, i.e., last day of the forecast target week in M/D/YYYY format
 
national – error for national forecast (calculated using log difference)
 
covid_complete_national_score - The national forecast score assigned by CovidComplete
 
num_state_point_forecasts – number of states forecast by the model
 
log_difference_squared – sum of the squares of log differences for each state forecast; for values < 0 substitute values of 0.5 are used
 
pearson_fit_statistic – sum of (Actual–Forecast)^2/Actual; for actuals = 0, substitute values of 0.5 are used. 
 
mean_absolute_error – arithmetic average of the absolute errors in the state forecasts
 
geo_mean_log_difference – geometric mean of the log differences
 
median_log_difference – median error in log differences

balanced_relative_error - arithmetic average of state forecast errors, with individual errors calculated as max(forecast,actual)/min(forecast,actual)-1. for values = 0, substitute values of 0.5 are used. 

pred_25 - percentage of state forecasts within 25% of actual value. The 25% threshhold for overestimates is calculated as 25% of the actual value. For underestimates it is calculated as 1/1.25 or 80% of the actual value. 
 
missed_by_2x – percentage of state forecasts that missed by more than 200% of actual value, e.g., for an actual value of 1, forecast values of > 3. 
 
covid_complete_state_point_score - total score for state point forecasts awarded by CovidComplete.  

num_state_range_forecasts - number of states for which the model forecasts prediction intervals

successful_ranges - percentage of prediction intervals that capture the actual value

ranges_gt_4x - percentage of prediction intervals in which the p(0.975) / p(0.025) > 4.49 (i.e., the wide of the range rounds to greater than 4). 
 
ranges_gt_10x - percentage of prediction intervals in which the p(0.975) / p(0.025) > 10.49 (i.e., the wide of the range rounds to greater than 10). 

covid_complete_state_range_score - The state range score assigned by CovidComplete.  

# Covid Complete Scoring
 
covid_complete_national_score - National scores are allocated as 100% for forecasts within 5% of actual, 90% for forecasts within 10% of actual, 75% for forecasts within 25% of actual, 0% for other forecasts. 

covid_complete_state_point_score - This is a weighted score allocated as follows: log_difference_squared (1), geo_mean_log_difference (1), pearson_fit_statistic (0.75), median_log_difference (0.75), pred_25 (0.5), missed_by_2x (0.5), mean_absolute_error (0.25). In addition, models that forecast fewer than 51 states' have their scores for log_difference_squared and pearson_fit_statistic adjusted. The adjustment is (x^51)^(1/(num_states-1)). Conceptually, this is Bessel's correction for an unbiased estimator, applied to the geometric mean. Scores are relative among models within a forecast date and forecast target; the highest possible score for any forecast set is defined as the highest pred(25) value of the set divided by 0.75. The score for each factor is set at 100% for the best model performance for each factor and 0% for the 25th percentile model performance for each factor. 

covid_complete_state_range_score - This is the number of ranges that are <=4x wide that successfully include the actual value, divided by 0.95. A model whose prediction intervals include 95% of actual values with ranges <=4x will score 100%.  

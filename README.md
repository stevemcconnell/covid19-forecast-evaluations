# Covid19 Forecast Evaluations

Evaluations of forecasts that have been submitted to Covid-hub in support of the CDC's Ensemble model for Covid-19 death forecasts.

Unless otherwise noted, all "errors" in the files refer to "log difference", which is calculated as ln(forecast/actual) -- which mathematically is the same as ln(forecast) - ln(actual), which is why it's called log difference. 

Only incremental forecasts are scored. 

Within a forecast set for a particular forecast date, the incremental error numbers are  cumulative for the forecast date, meaning the Forecasts for Week 2 are the incremental forecasts for Wk1+Wk2, which are compared to the actuals for Wk1+Wk2, etc.

"Baseline" forecasts are included. The baseline is the average deaths for the 2 weeks preceding the first date of the forecast period. The baseline of 2 weeks preceding has been more accurate than the baseline of 1 week preceding.

# Columns

Here’s a description of the csv file contents, by column header:
 
model – The CDC covid-hub model name
 
forecast_date – The CDC covid-hub forecast date for the summary files in M/D/YYYY format
 
target - The CDC covid-hub target period, i.e., 1 wk ahead inc death, 2 wk ahead inc death, etc. Only incremental targets are contained in these files. 

target_week_end  – The CDC target week end, i.e., last day of the forecast target week in M/D/YYYY format
 
national – Error for national forecast (calculated using log difference)
 
cc_national_score - The national forecast score assigned by CovidComplete
 
num_state_point_forecasts – Number of states forecast by the model
 
log_difference_squared – Sum of the squares of log differences for each state point forecast; for forecast values and/or actual values < 0, substitute values of 0.5 are used
 
pearson_fit_statistic – Sum of [(Actual–Forecast)^2]/Actual for state point forecasts; for actuals = 0, substitute values of 0.5 are used. 
 
mean_absolute_error – Arithmetic average of the absolute errors of the state point forecasts
 
geo_mean_log_difference – Geometric mean of the log differences of the point state forecasts
 
median_log_difference – Median error in log differences of the state point forecasts

balanced_relative_error - Arithmetic average of state point forecast errors, with individual errors calculated as max(forecast,actual)/min(forecast,actual)-1. for forecast and/or actual values = 0, substitute values of 0.5 are used. 

pred_25 - Percentage of state point forecasts within 25% of actual value. The 25% threshhold for overestimates is calculated as 25% of the actual value. For underestimates it is calculated as 1/1.25 or 80% of the actual value. 
 
missed_by_2x – Percentage of state forecasts that missed by more than 200% of actual value, e.g., for an actual value of 1, forecast values of > 2 or < 0.5
 
cc_state_point_score - Total score for state point forecasts awarded by CovidComplete.  

num_state_range_forecasts - Number of states for which the model forecasts prediction intervals

successful_ranges - Percentage of prediction intervals that capture the actual value in the 0.025 to 0.975 quantile range

ranges_gt_4x - Percentage of prediction intervals in which the p(0.975) / p(0.025) > 4.49, i.e., the width of the range rounds to greater than 4. 
 
ranges_gt_10x - Percentage of prediction intervals in which the p(0.975) / p(0.025) > 10.49, i.e., the width of the range rounds to greater than 10. 

cc_state_range_score - The state range score assigned by CovidComplete.  

cc_national_rank - Model rank within forecast set, 1 is best; NumForecastModels is worst

cc_national_percentile - Model percentile rank within forecast set, 100% is best; 0% is worst

cc_state_point_rank - Model rank within forecast set, 1 is best; NumForecastModels is worst

cc_state_point_percentile - Model percentile rank within forecast set, 100% is best; 0% is worst

cc_state_range_rank - Model rank within forecast set, 1 is best; NumForecastModels is worst

cc_state_range_percentile - Model percentile rank within forecast set, 100% is best; 0% is worst

# Covid Complete Scoring
 
covid_complete_national_score - National scores are allocated as 100% for forecasts within 5% of actual, 90% for forecasts within 10% of actual, 75% for forecasts within 25% of actual, 0% for other forecasts. 

covid_complete_state_point_score - This is a weighted score allocated as follows: log_difference_squared (1), geo_mean_log_difference (1), pearson_fit_statistic (0.75), median_log_difference (0.75), pred_25 (0.5), missed_by_2x (0.5), mean_absolute_error (0.25). In addition, models that forecast fewer than 51 states' have their scores for log_difference_squared and pearson_fit_statistic adjusted. The adjustment is (Score^(1/(num_states_forecast-1))^51. Conceptually, this is Bessel's correction for an unbiased estimator, applied to the geometric mean. Scores are relative among models within a forecast date and forecast target; the highest possible score for any forecast set is defined as the highest pred(25) value of the set divided by 0.75. The score for each factor is set at 100% for the best model performance for each factor and 0% for the 25th percentile model performance for each factor. 

covid_complete_state_range_score - This is the number of ranges that are <=4x wide that successfully include the actual value, divided by 0.95. A model whose prediction intervals include 95% of actual values with ranges <=4x will score 100%. Models that forecast fewer than 51 states have their score adjusted by Score*num_states_forecast/51. 

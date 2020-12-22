# Covid19 Death Forecast Evaluations

This site contains coronavirus forecast evaluation data for forecasts that have been submitted to Covid-hub in support of the CDC's Ensemble model for Covid-19 death forecasts. Graphs and reports in more human readable form are available on the CovidComplete website at https://stevemcconnell.com/cdc-covid-19-forecast-evaluations/. 

Column names are stable and will not change. Column positions are subject to change. 

## General contents of the Covid-19 forecast evaluation file

Unless otherwise noted, all "errors" in the files refer to "log difference", which is calculated as ln(forecast/actual), which mathematically is the same as ln(forecast) - ln(actual) (which is why it's called log difference). 

Some errors are presented as balanced relative error (BRE), which is calculated as max(forecast,actual)/min(forecast,actual)-1. For forecast and/or actual values = 0, substitute values of 0.5 are used. 

Only incremental coronavirus forecasts are included. 

Within a forecast set for a particular forecast date, the incremental error numbers are  cumulative for the forecast date, meaning the Forecasts for Week 2 are the incremental forecasts for Wk1+Wk2, which are compared to the actuals for Wk1+Wk2, etc.

"Baseline" forecasts are included. The baseline is the average deaths for the 2 weeks preceding the first date of the forecast period. (The baseline of 2 weeks preceding has been more accurate than the baseline of 1 week preceding.) There is no baseline for prediction intervals at this time. 

## Columns

Here’s a description of the csv file contents, by column header:
 
### General info
Field | Description
:---- | :----
model | The CDC covid-hub model name
forecast_date | The CDC covid-hub forecast date for the summary files in M/D/YYYY format
target | The CDC covid-hub target period, i.e., 1 wk ahead inc death, 2 wk ahead inc death, etc. Only incremental targets are contained in these files. 
target_week_end  | The CDC target week end, i.e., last day of the forecast target week in M/D/YYYY format
 
### National forecasts
Field | Description
:---- | :----
national_raw_error | Simple arithmetic difference between the national forecast and the national actual value
national_log_difference | Error for national forecast calculated using log difference
national_percentage_error | Simple arithmetic difference between the national forecast and the national actual value
national_bre | Balanced relative error of the national forecast

#### *CovidComplete national forecast scoring* 
Field | Description
:---- | :----
cc_national_score | The national forecast score assigned by CovidComplete
cc_national_rank | The model's national forecast rank within the current set of national forecasts
cc_national_rank_percentile | The model's national forecast rank expressed as a percentile of the ranking; 100% is best; 0% is worst

### State point forecasts
Field | Description
:---- | :----
state_point_forecasts_num | Number of states forecast by the model
state_log_difference_squared | Sum of the squares of log differences for each state point forecast; for forecast values and/or actual values < 0, substitute values of 0.5 are used
state_pearson_fit_statistic | Sum of [(Actual–Forecast)^2]/Actual for state point forecasts; for actuals = 0, substitute values of 0.5 are used. 
state_mean_absolute_error | Arithmetic average of the absolute errors of the state point forecasts
state_geo_mean_log_difference | Geometric mean of the absolute values of the log differences of the point state forecasts. Errors of 0 are multiplied as 1's. 
state_median_log_difference | Median error in log differences of the state point forecasts
state_bre | Arithmetic average of state point forecast errors, with individual errors calculated as balanced relative error. 
state_bre_signed | Same as state_bre, except that underestimates receive a negative sign
state_pred_25 | Percentage of state point forecasts within 25% of actual value. The 25% threshhold for overestimates is calculated as 25% of the actual value. For underestimates it is calculated as 1/1.25 or 80% of the actual value. 
state_missed_by_2x | Percentage of state forecasts that missed by more than 200% of actual value, e.g., for an actual value of 1, forecast values of > 2 or < 0.5
state_rmse | Root mean squared error (RMSE) of state forecasts
state_mape | Mean absolute percentage error (MAPE) of state forecasts. MAPE is calculated as the mean of abs(actual-forecast)/actual. 
state_smape | Symmetric mean absolute percentage error (SMAPE) of state forecasts. SMAPE is calculated as the mean of abs(actual-forecast)/((actual+forecast)/2)

#### *CovidComplete state point forecast scoring*
Field | Description
:---- | :----
cc_state_point_score | Total score for state point forecasts awarded by CovidComplete.  
cc_state_point_rank | The model's state point  forecast rank within the current set of state point forecasts
cc_state_point_rank_percentile | The model's state point forecast rank expressed as a percentile of the ranking; 100% is best; 0% is worst

### State range forecasts
Field | Description
:---- | :----
state_range_forecasts_num | Number of states for which the model forecasts prediction intervals (PIs)
state_successful_ranges | Percentage of prediction intervals that capture the actual value in the 0.025 to 0.975 quantile range

For the following fields, "width" is defined as the 0.975 PI quantile divided by the 0.025 quantile. 
Field | Description
:---- | :----
state_range_10th_percentile_width | 10th percentile of PI widths, i.e., width of narrowest ranges
state_range_25th_percentile_width | 25th percentile of PI widths
state_range_50th_percentile_width | 50th percentile of PI widths, i.e., median range width
state_range_average_width | average range width; some range widths are extreme, so median and average can be significantly different
state_range_75th_percentile_width | 75th percentile of PI widths
state_range_90th_percentile_width | 90th percentile of PI widths, i.e., width of widest ranges
state_ranges_gt_4x | Percentage of prediction intervals in which the p(0.975) / p(0.025) > 4.49, i.e., the width of the range rounds to greater than 4. 
state_ranges_gt_10x | Percentage of prediction intervals in which the p(0.975) / p(0.025) > 10.49, i.e., the width of the range rounds to greater than 10. 
state_ranges_interval_score | Interval score for the 95% prediction intervals ala Gneiting and Raftery. This is the sum of all the state interval scores. Note, this is not the weighted interval score, just the interval score for the 95% PI. 
state_ranges_interval_normalized | Average interval score for the 95% prediction intervals in which the interval score for each state is divided by the actual for each state.  
state_ranges_precision_raw | Average precision score for each 95% prediction interval calculated as (upper-lower) / (upper+lower). For forecast and/or actual values = 0, substitute values of 0.5 are used. See notes on CovidComplete range score v. 2 below. 
state_ranges_precision_95pi_adjusted | Average precision score adjusted for the precision that's possible withi 95% PIs. 

#### *CovidComplete state range  forecast scoring*
Field | Description
:---- | :----
cc_state_range_score | The state range score assigned by CovidComplete.  
cc_state_range_score_v2 | Version 2 of the state range score assigned by CovidComplete. See notes on CovidComplete range score v. 2 below.
cc_state_range_rank | Model rank within forecast set, 1 is best; NumForecastModels is worst
cc_state_range_rank_percentile | Model percentile rank within forecast set, 100% is best; 0% is worst
cc_state_range_rank_v2 | Model rank within forecast set, 1 is best; NumForecastModels is worst
cc_state_range_rank_percentile_v2 | Model percentile rank within forecast set, 100% is best; 0% is worst

## Covid Complete Scoring

### covid_complete_national_score
National scores are allocated as 100% for forecasts within 5% of actual, 90% for forecasts within 10% of actual, 75% for forecasts within 25% of actual, 0% for other forecasts. 

### covid_complete_state_point_score
This is a weighted score allocated as follows: log_difference_squared (1), geo_mean_log_difference (1), pearson_fit_statistic (0.75), median_log_difference (0.75), pred_25 (0.5), missed_by_2x (0.5), mean_absolute_error (0.25). In addition, models that forecast fewer than 51 states' have their scores for log_difference_squared and pearson_fit_statistic adjusted before those factors are including in the state point score. The adjustment is (Score^(1/(num_states_forecast-1))^51. Conceptually, this is Bessel's correction for an unbiased estimator, applied to the geometric mean. 

Scores are relative among models within a forecast date and forecast target; the highest possible score for any forecast set is defined as the highest pred(25) value of the set divided by 0.75. The score for each factor is set at 100% for the best model performance for each factor and 0% for the 25th percentile model performance for each factor. 

### covid_complete_state_range_score
This score is accuracy-limited. A model cannot score higher than its capture rate. Models are penalized for poor precision (wide ranges), so a model will score lower than its capture rate if it uses wide ranges. 

Score is calculated as the percentage of ranges that are <=4x wide that successfully include the actual value, divided by 0.95. A model whose prediction intervals include 95% of actual values with ranges <=4x will score 100%. Models that forecast fewer than 51 states have their score adjusted by Score * num_states_forecast/51.  

### covid_complete_state_range_score_v2
This score is also based on accuracy first, precision second. It is accuracy-limited, and the precision penalty is more fine-grained than version 1's penalty. 

**state_ranges_precision_raw** is defined as 1-(upper-lower)/(upper+lower), with values of 0.5 subsituted for values of 0. For ranges in which upper=lower (i.e., point forecasts), precision will be 1.0, or 100%. Worst precision is asymptotic at 0%. This measure of precision is affected by width of the PI range but it is intentionally not affected by the location of the actual value within the range. Similarly, it is also not affected by the degree to which a range misses an actual value, only by the width of the range itself. The possible values for precision thus range from 0-100%, regardless of scale. 

**state_ranges_precision_95pi_adjusted** Calibration has determined a 95% capture rate with raw precision higher than about 47.9% is not possible, so the adjusted precision score is the raw precision score adjusted for the precision needed to attain the intended level of 95% PI coverage. The adjusted precision score is thus raw precision score / 0.479, where 0.479 is a constant that is derived through calibration. For practical purposes, this constant can be estimated using the formula 1 - IGR + IGR * alpha^IGR, where IGR is the inverse golden ratio and alpha is 1 - prediction interval. The adjusted precision score is limited to a max of 100%. 

**covid_complete_state_range_score_v2** is calculated as the PI capture rate / 0.95, limited to a max of 1.0 (i.e., 100% credit for capture of 95%, and no extra credit for capture rates higher than 95%); minus (1-adjusted precision)^2. This penalizes precision close to 100% minimally and penalizes lower precision disproportionately. 
* A model with 95% capture rate and an adjusted precision score of 100% will score 100%. 
* A model with 100% capture rate and an adjusted precision score of 100% will score 100%. 
* A model with 95% capture rate and an adjusted precision score of 75% will score 94%. 
* A model with 95% capture rate and an adjusted precision score of 50% will score 75%. This model's score will be equal to a model with a 71% capture rate (which receives a base score of 75% (0.71/0.95=0.75)) and a 100% precision score. 
* A model with a 71% capture rate and an adjusted precision score of 50% will score 54%. 
* A model with a 95% capture rate and an adjusted precision score of 0% (i.e., a model that guesses zero to 1 million for everything) will score 0%. 

This scoring approach favors accuracy first, precision second, and does not allow models with high precision but moderate accuracy to outperform models with high accuracy and only moderate precision.

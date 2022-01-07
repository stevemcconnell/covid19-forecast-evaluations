# Covid19 Death Forecast Evaluations

This site contains  forecast evaluations for forecasts submitted to Covid-hub in support of the CDC's Ensemble model for Covid-19 death forecasts. Graphs and reports in more human readable form are available on the CovidComplete website at https://stevemcconnell.com/cdc-covid-19-forecast-evaluations/. 

Column names are stable and will change infrequently or not at all. Column positions are subject to change. 

The Excel spreadsheets are  powerful in terms of allowing models to be sorted and filtered by the performance metrics described below. 

## General contents of the Covid-19 forecast evaluation file

Unless otherwise noted, all "errors" in the files refer to "log difference", which is calculated as ln(forecast/actual). Mathematically, that is the same as ln(forecast) - ln(actual), which is why it's called log difference. For forecast and/or actual values = 0, substitute values of 0.5 are used. 

Some errors are presented as balanced relative error (BRE), which is calculated as max(forecast,actual)/min(forecast,actual)-1. For forecast and/or actual values = 0, substitute values of 0.5 are used. 

Evaluations are based on the forecast teams' submitted incident coronavirus forecasts. The evaluations of "cumulative" forecasts are based on the sums of the incident forecasts, rather than the submitted cumulative forecasts, i.e., the forecasts for Week 2 are the incident forecasts for Wk1+Wk2, which are compared to the actuals for Wk1+Wk2, etc.

"Baseline" forecasts are included. The **baseline point forecast** is the average deaths for the 2 weeks preceding the first date of the forecast period. The baseline of average deaths for 2 weeks preceding has been slightly more accurate than the baseline of 1 week preceding. **The 'Baseline' forecasts are based on the historical data that was available close to the time of the forecasts,** i.e., the Baseline forecasts do not make use of updates that were available after the forecast date.  

The **baseline prediction interval** forecast is the range from 50% of the baseline point forecast to 200% of the baseline point forecast. 

"Dynamic baseline forecasts" are also included. These forecasts are named "Baseline" and appended with the abbreviated name of the evaluation data set, such as "Baseline-CDC". The dynamic baseline forecasts are constructive from  data that is currently available. Thus Baseline and Baseline-JHU-U will not always match, because of updates that have been made to the JHU CSSE data between the time the original baseline for a forecast period was constructed and the present. 

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
national_raw_error | Simple arithmetic difference between the national forecast and the national actual value. Because actual values vary significantly over time, evaluating models that provided forecasts over different time periods can be misleading. Evaluations will be most accurate if time periods are aligned when evaluating different models on this metric.
national_log_difference | Error for national forecast calculated using log difference
national_percentage_error | (forecast - actual) / actual
national_bre | Balanced relative error of the national forecast

#### *CovidComplete national forecast scoring* 
Field | Description
:---- | :----
cc_national_score | The national forecast score assigned by CovidComplete
cc_national_rank | The model's national forecast rank within the current set of national forecasts
cc_national_rank_percentile | The model's national forecast rank expressed as a percentile of the ranking; 100% is best; 0% is worst 
CovidComplete's scoring formula is described below. 

### State point forecasts
Field | Description
:---- | :----
state_point_forecasts_num | Number of states forecast by the model
state_log_difference_squared | Sum of the squares of log differences for each state point forecast; for forecast values and/or actual values <= 0, substitute values of 0.5 are used. Because this metric depends on the magnitudes of the actual values, care should be taken when comparing values across time periods in which the values of the actuals vary. 
state_log_difference_squared_rank_percentile | The model's state log difference squared error rank within a set of forecasts expressed as a percentile of the ranking; 100% is best; 0% is worst
state_pearson_fit_statistic | Sum of [(Actual–Forecast)^2]/Actual for state point forecasts; for actuals = 0, substitute values of 0.5 are used. Because this metric depends on the magnitudes of the actual values, care should be taken when comparing values across time periods in which the values of the actuals vary. 
state_pearson_fit_rank_percentile | The model's state pearson fit error rank within a set of forecasts expressed as a percentile of the ranking; 100% is best; 0% is worst
state_mean_absolute_error | Arithmetic average of the absolute errors of the state point forecasts. This metric is an indication of the magnitude of error in forecasts. However, because this metric depends on the magnitudes of the actual values, care should be taken when comparing values across time periods in which the values of the actuals vary. 
state_mean_absolute_error_rank_percentile | The model's state mean absolute error rank within a set of forecasts expressed as a percentile of the ranking; 100% is best; 0% is worst
state_relative_mae | Relative mean absolute error (MAE) as defined in the covidhub forecast evaluation work. This metric is constructed using pairwise comparisons, state by state, between each pair of models. Note that the relative MAE in these evaluations is normalized using the Dynamic Baseline for each evaluation data set. The relative MAEs for models when the Uncorrected JHU evaluation data set is used should be directly comparable to relative MAEs published in the forecast hub evaluation work. Relative MAEs for evaluations based on other evaluation data sets will not be comparable.  
state_geo_mean_log_difference | Geometric mean of the absolute values of the log differences of the point state forecasts. Errors of 0 are multiplied as 1's. This metric indicates the magnitude of forecast error.  
state_geo_mean_log_difference_rank_percentile | The model's state geometric mean of log difference error rank within a set of forecasts expressed as a percentile of the ranking; 100% is best; 0% is worst
state_median_log_difference | Median error in log differences of the state point forecasts. This metric indicates bias in forecasts. 
state_bre | Arithmetic average of state point forecast errors, with individual errors calculated as balanced relative error. This metric indicates the magnitude of forecast error. 
state_bre_signed | Same as state_bre, except that underestimates receive a negative sign
state_bre_rank_percentile | The model's state unsigned bre error rank within a set of forecasts expressed as a percentile of the ranking; 100% is best; 0% is worst
state_pred_25 | Percentage of state point forecasts within 25% of actual value, typically expressed as pred(25). The 25% threshhold for overestimates is calculated as 25% of the actual value. For underestimates it is calculated as 1/1.25 or 80% of the actual value. 
state_pred25_rank_percentile | The model's state pred(25) error rank within a set of forecasts expressed as a percentile of the ranking; 100% is best; 0% is worst
state_missed_by_2x | Percentage of state forecasts that missed by more than 200% of actual value, e.g., for an actual value of 1, forecast values of > 2 or < 0.5
state_rmse | Root mean squared error (RMSE) of state forecasts. This metric indicates the magnitude of forecast error. Because this metric depends on the magnitudes of the actual values, care should be taken when comparing values across time periods in which the values of the actuals vary. 
state_rmse_rank_percentile | The model's state rmse error rank within a set of forecasts expressed as a percentile of the ranking; 100% is best; 0% is worst
state_mape | Mean absolute percentage error (MAPE) of state forecasts. MAPE is calculated as the mean of abs(actual-forecast)/actual. 
state_mape_rank_percentile | The model's state mape error rank within a set of forecasts expressed as a percentile of the ranking; 100% is best; 0% is worst
state_smape | Symmetric mean absolute percentage error (SMAPE) of state forecasts. SMAPE is calculated as the mean of abs(actual-forecast)/((actual+forecast)/2)
state_smape_rank_percentile | The model's state smape error rank within a set of forecasts expressed as a percentile of the ranking; 100% is best; 0% is worst
state_theilu2 | Theil's U2 statistics for state forecasts. Theil's U2 statistic is essentially a baseline forecast that, rather than using the static value of the prior period, uses the magnitude of change from the prior period and the period before that.  
state_theilu2_rank_percentile | The model's state Theil U2 error rank within a set of forecasts expressed as a percentile of the ranking; 100% is best; 0% is worst

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
state_range_capture_rate_95PI | Percentage of 95% prediction intervals that capture the actual value in the 0.025 to 0.975 quantile range
state_range_capture_rate_50PI | Percentage of 50% prediction intervals that capture the actual value in the 0.25 to 0.75 quantile range
state_range_10th_percentile_width | 10th percentile of PI widths, i.e., width of narrowest ranges. In this field and the following fields, "width" is defined as the 0.975 PI quantile divided by the 0.025 quantile, with the value of 0.5 subsituted for the value of 0 where necessary. 
state_range_25th_percentile_width | 25th percentile of PI widths
state_range_50th_percentile_width | 50th percentile of PI widths, i.e., median range width
state_range_average_width | average range width; some range widths are extreme, so median and average can be significantly different
state_range_75th_percentile_width | 75th percentile of PI widths
state_range_90th_percentile_width | 90th percentile of PI widths, i.e., width of widest ranges
state_ranges_gt_4x | Percentage of prediction intervals in which the p(0.975) / p(0.025) > 4.49, i.e., the width of the range rounds to greater than 4. 
state_ranges_gt_10x | Percentage of prediction intervals in which the p(0.975) / p(0.025) > 10.49, i.e., the width of the range rounds to greater than 10. 
state_ranges_95PI_score | Interval score for the 95% prediction intervals ala Gneiting and Raftery. This is the sum of the individual state interval scores. Note, this is not the weighted interval score, but the interval score for the 95% PI. 
state_ranges_50PI_score | Interval score for the 50% prediction intervals ala Gneiting and Raftery. This is the sum of the individual state interval scores. Note, this is not the weighted interval score, but the interval score for the 50% PI. 
state_ranges_interval_normalized | Average interval score for the 95% prediction intervals in which the interval score for each state is divided by the actual for each state.  
state_ranges_synthetic_wis | Synthetic WIS (WIS) based on a subset of the quantiles provided by the forecast models. The subset WIS is based on the point forecast (0.5 quantile), 50% PI, and 95% PI. Synthetic WIS is within 2% of WIS calculated from the full set of quantiles. This is the sum of the individual state synthetic WIS scores. 
state_ranges_synthetic_wis_sharpness | Portion of the Synthetic WIS due to the sharpness (precision) score. 
state_ranges_synthetic_wis_penalty | Portion of the Synthetic WIS due to the penalty score. 
state_ranges_synthetic_wis_rank_percentile | The model's rank compared to other models that provided forecasts for that forecast period and target. 
state_relative_wis | Relative weighted interval score (WIS) as defined in the covidhub forecast evaluation work. This metric is constructed using pairwise comparisons, state by state, between each pair of models. Note that the relative WIS in these evaluations is normalized using the Dynamic Baseline for each evaluation data set. The relative WISs for models when the Uncorrected JHU evaluation data set is used should be directly comparable to relative WISs published in the forecast hub evaluation work. Relative WISs for evaluations based on other evaluation data sets will not be comparable.  
state_ranges_precision_raw | Average precision score for each 95% prediction interval. Precision is calculated as (upper-lower) / (upper+lower). For forecast and/or actual values = 0, substitute values of 0.5 are used. See notes on CovidComplete range score v. 2 below. 
state_ranges_precision_95pi_adjusted | Average precision score adjusted for the precision that's possible with 95% PIs. See CovidComplete scoring notes below for details. 

#### *CovidComplete state range  forecast scoring*
Field | Description
:---- | :----
cc_state_range_score | The state range score assigned by CovidComplete.  
cc_state_range_score_v2 | Version 2 of the state range score assigned by CovidComplete. See notes on CovidComplete range score v. 2 below.
cc_state_range_rank | Model rank within forecast set, 1 is best; NumForecastModels is worst
cc_state_range_rank_percentile | Model percentile rank within forecast set, 100% is best; 0% is worst
cc_state_range_rank_v2 | Model rank within forecast set, 1 is best; NumForecastModels is worst
cc_state_range_rank_percentile_v2 | Model percentile rank within forecast set, 100% is best; 0% is worst

### Evaluation Data Set Descriptions
**incident_or_cumulative** indicates whether evaluations are based on incident (1 week at a time) or cumulative (cumulative total from forecast date) forecasts. As described above, both incident and cumulative evaluations are based on the forecast teams' submitted incident coronavirus forecasts. The evaluations of "cumulative" forecasts are based on the sums of the incident forecasts, rather than the submitted cumulative forecasts. In other words, the forecasts for Week 2 are the incident forecasts for Wk1+Wk2, which are compared to the actuals for Wk1+Wk2, etc.

**evaluation_data_set** describes which data set was used to create the evaluations. The evaluation data sets are listed in order of preference: 
* **CDC Data Set** is data reported by the states to the CDC, pulled from the CDC data source at the time the evaluations were performed. This data set is a mix of "date of death" and "date of report" data. It is the preferred data set both because it contains the highest percentage of date of death data and because it is the CDC's data set of record. 
* **JHU Data Set—Full Corrections** this is data that has been reported by JHU CSSE, pulled from gitub at the time the evaluations were performed, corrected for known anomalies. Most of the anomalies consist of states reporting large numbers of deaths on one day as a result of death certificate reviews. In some instances, states routinely report deaths that occurred more than a month earlier (e.g., Oregon througout the fall of 2021). For this type of anomaly, only anomalies that have been verified by state agencies or local news sources are included. A secondary type of anomaly consists of states reporting negative numbers of deaths for a day or week. These are corrected whether verified or not. For both of the first two types of anomalies, the corrections are mechanical back distributions and are approximate. A tertiary type of correction is substitions of data directly from a state data source, when the state-reported data is believed to be more accurate than the JHU CSSE data (e.g., Ohio throughout the second half of 2021). A quartenary type of correction is substitution of CDC data when that data is believed to be more accurate than the JHU CSSE data (e.g., Florida, North Carolina, Texas, Virginia, and Wisconsin throughout 2021). 
* **NYT Data Set** is data reported by the New York Times, pulled from the NYT github site at the time the evaluations were peformed. 
* **JHU Data Set—Uncorrected** is the uncorrected JHU data that was pulled from gitub at the time the evaluations were performed. 

## Covid Complete Scoring

### covid_complete_national_score
National scores are allocated as 100% for forecasts within 5% of actual, 90% for forecasts within 10% of actual, 75% for forecasts within 25% of actual, 0% for other forecasts. 

### covid_complete_state_point_score
This is a weighted score allocated as follows: log_difference_squared (1), geo_mean_log_difference (1), pearson_fit_statistic (0.75), median_log_difference (0.75), pred_25 (0.5), missed_by_2x (0.5), mean_absolute_error (0.25). The measures of log_difference_squared and pearson_fit_statistic are affected by the number of states forecast, so models that forecast fewer than 51 states might appear to be more accurate compared to other models than they are.  

Scores are relative among models within a forecast date and forecast target; the highest possible score for any forecast set is defined as the highest pred(25) value of the set divided by 0.75. The score for each factor is set at 100% for the best model performance for each factor and 0% for the 25th percentile model performance for each factor. 

The total possible score is limited by the best pred(25) score in each forecast set, using the formula MaxPossibleScore = BestPred25Score / 0.75, with maximum limited to 100%. The preliminary score for each model is multiplied by MaxPossibleScore. If any model scores 75% or better on pred(25), then the maximum score possible is 100%. As of this writing, pred(25) has exceeded the 75% threshold 0.06% of the time. If the best pred(25) score within a given forecast set is lower than 75%, then the maximum possible score will be less than 100%. 

### covid_complete_state_range_score_v2
This score is based on accuracy first, precision second. It is accuracy-limited.  

**state_ranges_precision_raw** is defined as 1-(upper-lower)/(upper+lower), with values of 0.5 subsituted for values of 0. For ranges in which upper=lower (i.e., point forecasts), precision will be 1.0, or 100%. Worst precision is asymptotic at 0.0%. This measure of precision is affected by width of the PI range but, by design, it is not affected by the location of the actual value within the range. Similarly, it is also not affected by the degree to which a range misses an actual value, only by the width of the range itself. The possible values for precision thus range from 0-100%, regardless of magnitude of the forecast values or actual value. 

**state_ranges_precision_95pi_adjusted** Calibration has determined a 95% capture rate with raw precision higher than about 48% is not possible, so the adjusted precision score is the raw precision score adjusted for the precision needed to attain the intended level of 95% PI coverage. The adjusted precision score is thus raw precision score / 0.479, where 0.479 is a constant that is derived through calibration. The adjusted precision score is limited to a max of 100%. 

**covid_complete_state_range_score_v2** is calculated as the PI capture rate / 0.95, limited to a max of 1.0 (i.e., 100% credit for capture of 95%, and no extra credit for capture rates higher than 95%); minus (1-adjusted precision)^2. This penalizes precision close to 100% minimally and penalizes lower precision disproportionately. 
* A model with 95% capture rate and an adjusted precision score of 100% will score 100%. 
* A model with 100% capture rate and an adjusted precision score of 100% will score 100%. 
* A model with 95% capture rate and an adjusted precision score of 75% will score 94%. 
* A model with 95% capture rate and an adjusted precision score of 50% will score 75%. This model's score will be equal to a model with a 71% capture rate (which receives a base score of 75% (0.71/0.95=0.75)) and a 100% precision score. 
* A model with a 71% capture rate and an adjusted precision score of 50% will score 54%. 
* A model with a 95% capture rate and an adjusted precision score of 0% (i.e., a model that guesses zero to 1 million for everything) will score 0%. 

This scoring approach favors accuracy first, precision second, and does not allow models with high precision but moderate accuracy to outperform models with high accuracy and only moderate precision.

### covid_complete_state_range_score (deprecated)
This score is accuracy-limited. A model cannot score higher than its capture rate. Models are penalized for poor precision (wide ranges), so a model will score lower than its capture rate if it uses wide ranges. 

Score is calculated as the percentage of ranges that are <=4x wide that successfully include the actual value, divided by 0.95. A model whose prediction intervals include 95% of actual values with ranges <=4x will score 100%. Models that forecast fewer than 51 states have their score adjusted by Score * num_states_forecast/51.  


---
title: "Machine learning functions overview"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Machine-learning-functions-overview"
---

This topic lists the machine learning functions supported by Torch Log Service (TLS).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, the machine learning functions are in public beta.</div>


<span id="49bf213d"></span>
## Prediction and anomaly detection functions


|Function |Description |
|---|---|
|[ts_anomaly_filter](https://docs.byteplus.com/docs/tls/Prediction-and-anomaly-detection-functions#637de467) |Screens the anomaly detection results through customized anomaly patterns, so as to efficiently locate the abnormal curves. |
|[ts_predicate_simple](https://docs.byteplus.com/docs/tls/Prediction-and-anomaly-detection-functions#e991edcf) |Completes data modeling through default parameters to perform data prediction and outlier detection. |
|[ts_predicate_ar](https://docs.byteplus.com/docs/tls/Prediction-and-anomaly-detection-functions#d605c86e) |Completes data modeling through the autoregressive model to perform data prediction and outlier detection. |
|[ts_predicate_arima](https://docs.byteplus.com/docs/tls/Prediction-and-anomaly-detection-functions#a48307ec) |Predicts time series data with periodicity accurately. |
|[ts_regression_predict](https://docs.byteplus.com/docs/tls/Prediction-and-anomaly-detection-functions#234f0d00) |Filters the anomaly detection results based on the defined anomaly pattern after performing anomaly detection on time series data, which helps to quickly find the anomaly curve. |


<span id="d089ae85"></span>
## Time series clustering function


|Function |Description |
|---|---|
|[ts_density_cluster](https://docs.byteplus.com/docs/tls/Time-series-clustering-functions#2c8462cc) |Uses the density clustering method to cluster multiple time series curves. |
|[ts_hierarchical_cluster](https://docs.byteplus.com/docs/tls/Time-series-clustering-functions#3e2775b1) |Uses a hierarchical clustering method to cluster multiple time series curves. |
|[ts_similar_instance](https://docs.byteplus.com/docs/tls/Time-series-clustering-functions#4873c444) |Searches for time series curves that are similar to the specified time series curve. |


<span id="90b3b043"></span>
## Abnormal comparison function


|Function |Description |
|---|---|
|[anomaly_compare](https://docs.byteplus.com/docs/tls/Abnormal-comparison-function#cb7b66c2) |Compares the degree of difference between the target observation objects in the two time periods. |


<span id="6d989f5f"></span>
## Threshold recommendation function


|Function |Description |
|---|---|
|[ts_threshold_recommendation](https://docs.byteplus.com/docs/tls/Threshold-recommendation-function#7cdd228e) |Performs cluster analysis on historical time series data to quickly identify the distribution of normal data from the historical data. |


<span id="d9e48772"></span>
## Difference Pattern Statistical Function


|Function |Description |
|---|---|
|[pattern_diff](https://docs.byteplus.com/docs/tls/Difference-Pattern-Statistical-Function#4e0fafb1) |Based on the given field samples and judgment conditions, analyze the set of difference patterns defined by these conditions. |

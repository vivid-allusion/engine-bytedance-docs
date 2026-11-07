---
title: "Prediction and anomaly detection functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Prediction-and-anomaly-detection-functions"
---

This topic describes the syntax of prediction and anomaly detection functions supported by Torch Log Service(TLS) and examples of usage in common scenarios.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, the machine learning functions are in public beta.</div>


<span id="d9a7d5d1"></span>
## Function list


|Function |Description |
|---|---|
|ts_anomaly_filter |Screens the anomaly detection results through customized anomaly patterns, so as to efficiently locate the abnormal curves. |
|ts_predicate_simple |Completes data modeling through default parameters to perform data prediction and outlier detection. |
|ts_predicate_ar |Completes data modeling through the autoregressive model to perform data prediction and outlier detection. |
|ts_predicate_arima |Predicts time series data with periodicity accurately. |
|ts_regression_predict |Filters the anomaly detection results based on the defined anomaly pattern after performing anomaly detection on time series data, which helps to quickly find the anomaly curve. |


<span id="637de467"></span>
## ts_anomaly_filter

ts_anomaly_filter function is used to screen the anomaly detection results through customized anomaly patterns, so as to efficiently locate the abnormal curves.

<span id="3872e538"></span>
### Function syntax


* Syntax format

   ```SQL
   select ts_anomaly_filter(lineName, ts, ds, preds, probs, nWatch, anomalyType)
   ```
   

* Parameter description

   
   |Parameter |Data type |Description |
   |---|---|---|
   |lineName |varchar |The name of the curve. |
   |ts |array（double） |The time series, which is the time information of the current curve, is arranged in ascending order. |
   |ds |array（double） |The sequence of actual values, that is, the numerical information of the current curve. The length must be equal to the `ts` parameter. |
   |preds |array（double） |The predicted value sequence is the predicted value of the current curve. The length must be equal to the `ts` parameter. |
   |probs |array（double） |The anomaly detection sequence, that is, the anomaly detection result of the current curve. The length must be equal to the `ts` parameter. |
   |nWatch |long |The actual number of recently observed values in the current curve should be less than the actual curve length, that is, less than the length of the `ts` parameter. |
   |anomalyType |long |The type of exception is filtered.<br><br><br>* 0: All exceptions.<br><br>* 1: The rising edge is abnormal.<br><br>* \-1: The falling edge is abnormal. |
   

* Return value description

   If the input value is null, null will be returned.


<span id="53ec5569"></span>
### Function example


* Query and analysis statement

   ```SQL
   *| SELECT res.name, res.ts, res.ds, res.preds, res.probs  FROM (select ts_anomaly_filter(name, ts, ds, preds, probs, cast(1 as bigint), cast(1 as bigint)) as res 
          from (
            select 'aa' as name, array[1731294220,1731294221,1731294222] as ts, array[1,2,3] as ds, array[3,2,1] as preds, array[4,4,4] as probs ))
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ac8c027bbf1341d69bd5a63d54260abb~tplv-goo7wpa0wc-image.image) </span>


<span id="e991edcf"></span>
## **ts_predicate_simple**

ts_predicate_simple function completes data modeling through default parameters to perform data prediction and outlier detection.

<span id="dd30d08a"></span>
### Function syntax


* Syntax format

   ```SQL
   ts_predicate_simple(x, y, nPred, isSmooth) 
   ```
   

* Parameter description

   
   |Parameter |Data type |Description |
   |---|---|---|
   |x |String |The column name of the time column. The format is Unixtime timestamp in seconds. |
   |y |String |The column name of the numeric column, corresponding to the data at a certain time. |
   |nPred |Long |The number of future data points. The value is greater than or equal to 1. |
   |isSmooth |Boolean |Whether you need to filter the original data source.<br><br>The default is true, indicating filtering operations on the original data source. |
   

* Return value description

   If the input value is null, null will be returned.


<span id="08d070d2"></span>
### Function example


* Query and analysis statement

   ```SQL
   *| SELECT ts_predicate_simple(stamp, value, 10) FROM(SELECT stamp, value LIMIT 500)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/969e4f5b34c54122bb997c5cf7e47bb6~tplv-goo7wpa0wc-image.image) </span>

   
   |result column |explain |
   |---|---|
   |unixtime |The time column, with the unit of seconds. |
   |src |Original data. |
   |predict |The data obtained through prediction. |
   |upper |The upper bound of the predicted data. The current confidence level is fixed at 0.85. |
   |lower |The lower bound of the predicted data. The current confidence level is fixed at 0.85. |
   |anomaly_prob |The probability that the data point is an outlier. |
   


<span id="d605c86e"></span>
## **ts_predicate_ar**

ts_predicate_ar function completes data modeling through the autoregressive model to perform data prediction and outlier detection.

<span id="7eb86993"></span>
### Function syntax


* Syntax format

   ```SQL
   ts_predicate_ar(x, y, p, nPred, isSmooth) 
   ```
   

* Parameter description

   
   |Parameter |Data type |Description |
   |---|---|---|
   |*x* |String |The column name of the time column. The format is Unixtime timestamp in seconds. |
   |*y* |String |The column name of the numeric column, corresponding to the data at a certain time. |
   |p |Long |The order of the autoregressive model. The range of values is 2 to 8. |
   |nPred |Long |The number of future data points. The range of values is 1 to 5 \* *p.*  |
   |isSmooth |Boolean |Whether you need to filter the original data source.<br><br>The default is true, indicating filtering operations on the original data source. |
   

* Return value description

   If the input value is null, null will be returned.


<span id="0d4a1476"></span>
### Function example


* Query and analysis statement

   ```SQL
   *| SELECT ts_predicate_ar(stamp, value, 6,10) FROM(SELECT stamp, value LIMIT 500)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7d7b994954ec4d7da200bb6dfa238f64~tplv-goo7wpa0wc-image.image) </span>

   
   |result column |Description |
   |---|---|
   |unixtime |The time column, with the unit of seconds. |
   |src |The original data. |
   |predict |The data obtained through prediction. |
   |upper |The upper bound of the predicted data. The current confidence level is fixed at 0.85. |
   |lower |The lower bound of the predicted data. The current confidence level is fixed at 0.85. |
   |anomaly_prob |The probability that the data point is an outlier. |
   


<span id="a48307ec"></span>
## **ts_predicate_arima**

ts_predicate_arima function is used to accurately predict time series data with periodicity.

<span id="4063ba0f"></span>
### Function syntax


* Syntax format

   ```SQL
   ts_predicate_arima(x, y, p, d, q, nPred, isSmooth) 
   ```
   

* Parameter description

   
   |Parameter |Data type |Description |
   |---|---|---|
   |*x* |String |The column name of the time column. The format is unixtime timestamp in seconds. |
   |*y* |String |The column name of the numeric column, corresponding to the data at a certain time. |
   |p |Long |The order of the autoregressive model. The range of values is 2 to 8. |
   |d |Long |The order of the difference model. The range of values is 1 to 3. |
   |q |Long |The order of the moving average model. The range of values is 2 to 8. |
   |nPred |Long |The number of future data points. The range of values is 1 to 5 \* *p* . |
   |isSmooth |Boolean |Whether you need to filter the original data source.<br><br>The default is true, indicating filtering operations on the original data source. |
   

* Return value description

   If the input value is null, null will be returned.


<span id="f102a8b3"></span>
### Function example


* Query and analysis statement

   ```SQL
   *| SELECT ts_predicate_arima(stamp, value, 6,1,4,10) FROM(SELECT stamp, value LIMIT 500)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4f0a120e353641179379c3ce96e3a9aa~tplv-goo7wpa0wc-image.image) </span>

   
   |result column |Description |
   |---|---|
   |unixtime |The time column, with the unit of seconds. |
   |src |The original data. |
   |predict |The data obtained through prediction. |
   |upper |The upper bound of the predicted data. The current confidence level is fixed at 0.85. |
   |lower |The lower bound of the predicted data. The current confidence level is fixed at 0.85. |
   |anomaly_prob |The probability that the data point is an outlier. |
   


<span id="234f0d00"></span>
## ts_regression_predict

The ts_regression_predict function can filter the anomaly detection results based on the defined anomaly pattern after performing anomaly detection on time series data, which helps to quickly find the anomaly curve.

<span id="e54b2d5e"></span>
### Function syntax


* Syntax format

   ```SQL
   ts_regression_predict(x, y, nPred, algotype,processType)
   ```
   

* Parameter description

   
   |Parameter |Data type |Description |
   |---|---|---|
   |x |String |The name of the time column. The format is unixtime timestamp in seconds. |
   |y |String |The name of the numeric column corresponding to the data at a certain time. |
   |nPred |Long |The number of future data points. The range of values is from 1 to 500. |
   |algotype |String |Prediction algorithm types, optional values include:<br><br><br>* Origin: Prediction using GBRT (Gradient Boosted Regression Tree) algorithm.<br><br>* Forest: Using the results of STL sequence decomposition, the decomposed trend sequence is predicted using the GBRT algorithm, and then the decomposed sequence is summed according to the additive model and returned.<br><br>* Linear: Using the result of STL sequence decomposition, the decomposed trend sequence is predicted using the Linear Regression algorithm, and then the decomposed sequence is summed according to the additive model and returned. |
   |processType |String |Data preprocessing types, optional values include:<br><br><br>* 0: No additional data preprocessing is performed.<br><br>* 1: Abnormal data is removed before prediction. |
   

* Return value description

   If the input value is null, null will be returned.


<span id="bc4a16aa"></span>
### Function example


* Query and analysis statement

   ```SQL
   * | SELECT ts_regression_predict(stamp, value, 200, 'forest', 0) FROM(SELECT stamp, value LIMIT 500)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/182797f4b546465b892c3c1097923d97~tplv-goo7wpa0wc-image.image) </span>

   
   |result column |Description |
   |---|---|
   |unixtime |The Unix timestamp of the data. Unit: seconds. |
   |src |The Original data. |
   |predict |The data obtained through prediction. |

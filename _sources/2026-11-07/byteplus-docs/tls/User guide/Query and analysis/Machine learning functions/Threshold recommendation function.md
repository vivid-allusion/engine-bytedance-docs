---
title: "Threshold recommendation function"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Threshold-recommendation-function"
---

This article introduces the syntax of threshold functions supported by Torch Log Service(TLS) and usage examples in common scenarios.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, the machine learning functions are in public beta.</div>


<span id="7cdd228e"></span>
## ts_threshold_recommendation

Monitoring SLA\-related indicators by using the traditional method of manually configuring alarm rules has many shortcomings, including incomplete indicator coverage, inaccurate alarm thresholds, and so on. If the threshold for anomaly detection is configured too loosely, it will lead to a low rate of proactive fault discovery, and consequently, the user churn and compensation will increase. If the threshold for anomaly detection is configured too strictly, it will result in a large number of false positives, causing the operation and maintenance team to have no time to handle the real anomalies that occur.

The ts_threshold_recommendation function supports cluster analysis of historical time series data, quickly finds the distribution of normal data from the historical data, and automatically recommends anomaly detection thresholds. It can be used in scenarios such as alarm threshold setting.

<span id="0f340626"></span>
### **Function syntax**


* Syntax format

   ```SQL
   select ts_threshold_recommendation(x, y，metricType) 
   ```
   

* Parameter description

   
   |Parameter |Data type |Description |
   |---|---|---|
   |x |double |The time column is arranged in ascending order, with the format of unixtime timestamp and the unit of seconds. |
   |y |double |The numerical column corresponds to the values from a certain time. The length of the array needs to be the same as that of `x`, and the length of the array should be at least 500. |
   |metricType |varchar |* SuccessRate: Success rate. The input range of y is required to be from 0 to 1. If it is less than the recommended threshold, it is considered an anomaly.<br><br>* SuccessRate100: Success rate. The input range of y is required to be from 0 to 100. If it is less than the recommended threshold, it is considered an anomaly.<br><br>* ErrorRate: Error rate. The input range of y is required to be from 0 to 1. If it is greater than the recommended threshold, it is considered an anomaly.<br><br>* ErrorRate100: Error rate. The input range of y is required to be from 0 to 100. If it is greater than the recommended threshold, it is considered an anomaly.<br><br>* Count: Quantity statistics. The input range of y is required to be integers. If it is less than the recommended threshold, it is considered an anomaly.<br><br>* ErrorCount: The meaning of this indicator is error quantity statistics. The input range of y is required to be integers. If it is greater than the recommended threshold, it is considered an anomaly.<br><br>* Latency: Delay at the millisecond level. The input type of y is required to be a floating\-point number, and the unit is milliseconds. If it is greater than the recommended threshold, it is considered an anomaly.<br><br>* LatencySecond: Delay at the second level. The input type of y is required to be a floating\-point number, and the unit is seconds. If it is greater than the recommended threshold, it is considered an anomaly.<br><br>* ResourceUtilizationRate: Resource utilization rate. The input value range of y is required to be from 0 to 1. If it is greater than the recommended threshold, it is considered an anomaly.<br><br>* ResourceUtilizationRate100: Resource utilization rate. The input value range of y is required to be from 0 to 100. If it is greater than the recommended threshold, it is considered an anomaly.<br><br>* Output: Throughput. The input type of y is required to be a floating\-point number. If it is greater than the recommended threshold, it is considered an anomaly.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The difference between xxxRate and xxxRate100 is that when there are decimals in the data, xxxRate is selected, and when the data is an integer, xxxRate100 is selected.</div><br> |
   

* Return value description

   The return value is of the double type.


<span id="48e06160"></span>
### **Function example**


* Scenario

   Calculate millisecond latency thresholds based on time and request size.

* Query and analysis statement

   ```SQL
   *|select ts_threshold_recommendation(stamp, value, 'Latency')  from (select __time__ as stamp, ReqSize as value limit 1000)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/81386b5b13b94a28b43be9a62d8a3812~tplv-goo7wpa0wc-image.image) </span>

---
title: "View Function Metrics"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-View-Function-Metrics"
---

This document describes how to view the metrics of a function.

Metrics displays information such as the number of function executions, resource consumption, response events, and error counts. You can use this data to understand the function's performance and troubleshoot issues.

<span id="steps"></span>
## Steps

Follow these steps to view a function's metrics.


1. Open the [Functions](https://console.byteplus.com/cdn/edge-function/list) page.

2. Find the function for which you want to view metrics, and click on the function name.

3. Select the **Overview** tab. You can view the function's metrics on this page. Edge Functions default to displaying metrics for the past 24 hours. You can modify the time range to view data for any period within the past 7 days (accurate to the second).


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_c61b212275d79df5410aa8fff79590b8.jpeg) </span>

<span id="metrics-details"></span>
## Metrics details

Metrics includes statistical data and trend charts.

<span id="statistical-data"></span>
### Statistical data

Edge Functions allow you to view the following statistical data.


|Metric |Description |Unit |
|---|---|---|
|QPS |The number of function executions per second. |/ |
|Memory usage |The average memory consumption during function execution. |KB |
|CPU usage |The P95 value of CPU time for each request during function execution. |us |
|Response time |The P95 value of response time for each request during function execution. |ms |
|Error count |The rate of failed requests returned per second within the specified time range. Refer to [Invocation status](https://docs.byteplus.com/en/docs/18/20029#invocation-status) to understand the reasons for function request execution failures. |/ |


<span id="trend-charts"></span>
### Trend charts

Trend charts show the distribution of statistical data over time, i.e., the fluctuation of various metric data within the specified time period.

<span id="qps"></span>
#### QPS

The number of function executions per second.

<span id="response-time"></span>
#### Response time

The response time for each request.

<span id="cpu-usage"></span>
#### CPU usage

The CPU time of function execution within the specified time range.

<span id="memory-usage"></span>
#### Memory usage

The average memory consumption of the function within the specified time range.

<span id="response-status"></span>
#### Response status

The number of HTTP response status codes within the specified time range. For example, if the HTTP response status code is between [200,300), the count for 2xx responses increases by 1. The same applies to 3xx, 4xx, and 5xx.

If the response status code is not within [200,600), it is recorded as unknown.

<span id="invocation-status"></span>
#### Invocation status

The distribution of error statuses for function request executions.


* cpu_time_abort: Execution errors caused by CPU timeout.

* real_time_abort: Errors caused by response time timeout.

* memory_abort: Errors caused by memory exhaustion.

* other_abort: Indicates errors caused by abnormal client conditions, such as premature termination of requests by the client.

* error: Indicates other errors, such as unhandled exceptions in tenant code.

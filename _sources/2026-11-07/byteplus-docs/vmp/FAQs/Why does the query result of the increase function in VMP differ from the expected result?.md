---
title: "Why does the query result of the increase function in VMP differ from the expected result?"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Why_increase_function_in_VMP_differ_from_the-expected_result"
---

<span id="1Fznlcl0"></span>
## Issue description

When you use the increase function to query the total increments of counter\-type metrics, such as the request count, error count, restart count, and sent byte count, within a specified time range, the query result may differ from your expectations. The following section shows an example.

```Plain Text
increase(http_requests_total[5m])
sum(increase(http_requests_total{service="api"}[5m])) by (cluster)
```


<span id="ocXfdP6z"></span>
## Cause analysis

In VMP, when you query the total increments of counter\-type metrics within a specified time range, unexpected results are often caused by the usage of an inappropriate function instead of a fault. When you query the total increments of counter\-type metrics within a specified time range, the following three functions may be used: increase, increase_pure, and increase_prometheus.

For each query step, the query engine only performs calculations using the lookback window that corresponds to the step. Therefore, the first step may sometimes be 0 and sometimes not 0. For example, for `increase(x[5m])`, at 10:05, the system mainly analyzes samples around 10:00 to 10:05. If an available sample exists before the window, `increase()` will preferentially use the sample as the comparison baseline by default. If no sample exists before the window, increase() will not directly treat the first sample within the window as a 'newly added sample in this window' or as a 'historical value', but will determine this based on the changes between the first sample and subsequent samples.

By default, when no sample exists before the window, `increase()` will consider the incremental changes between the first point and subsequent points to determine whether the first value is a newly added value within the current window or an existing value before the window.


|**Sample form** |**Default determination method** |**Possible result** |
|---|---|---|
|The last sample exists before the window. |Directly use the sample before the window as the baseline value. |Whether the increment occurs within the current window can be determined more clearly. |
|No sample exists before the window. The first point has a small value, and subsequent increases are significant. |Similar to the scenario in which counters start from 0. |The first point may be counted as a newly added value in the current window. Therefore, the result may not be 0. |
|No sample exists before the window. The first point has a large value, and subsequent changes are small. |Similar to the scenario in which a historical value is re\-reported. |The first point may not be counted as a newly added value in the current window. Therefore, the result may be 0. |


<span id="ZOXCXOlZ"></span>
## Function selection suggestion

The differences among the three `increase` functions mainly lie in two aspects: how to assume the first point when no sample exists before the window, and whether to follow the Prometheus standard externally. Therefore, for routine queries, prioritize using `increase()`. To assume that the first value is 0, use `increase_pure()`. To keep the result consistent with that of native Prometheus, use `increase_prometheus()`.

The detailed descriptions are as follows:


|**Function** |**Method when no sample exists before the window** |**Whether to use Prometheus extrapolation** |**Applicable scenario** |Reason |
|---|---|---|---|---|
|increase() |Consider whether the first value is a new or historical value based on the incremental changes between the first point and subsequent points. |No |Routine queries and analysis in VMP. |By default, samples near the window boundaries are used to prevent counting the first sample that is clearly a historical value as a newly added value. |
|increase_pure() |Directly assume that the first value is 0. |No |Business scenarios in which the first value needs to be 0. |When no sample exists before the window, directly assume that counters start from 0. |
|increase_prometheus() |Calculate by using the Prometheus style and samples within the window. |Yes |Prometheus dashboard migration, alert compatibility verification, and standard difference troubleshooting. |Calculation is performed in the Prometheus style, including window extrapolation. The result may be a decimal. |


<span id="qFEvgX9v"></span>
## Solutions

When the query results do not match expectations, perform the following steps to troubleshoot, identify the issue, and select the function that is most suitable for the current usage scenario.


1. Check whether the metrics are counters. The function is not suitable for querying the increments of gauges.

2. Check the distribution of original samples. Focus on whether the last sample exists before the window. If no sample exists, observe the incremental changes between the first point and subsequent points.

3. Query both `increase()` and `increase_prometheus()` to determine whether the difference comes from Prometheus extrapolation.

4. Make sure that the range window is at least twice the collection interval. This prevents result instability caused by a small number of samples within the window.


```Bash
# The default VMP standard.
increase(my_counter_total[5m])

# The Prometheus-compatible standard.
increase_prometheus(my_counter_total[5m])

# The standard in which the first value is 0.
increase_pure(my_counter_total[5m])
```

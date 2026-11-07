---
title: "SQL time window syntax"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/sql_time_window_syntax"
---

When you create a scheduled SQL task, specify a SQL time window in the SQL rule configuration. The SQL time window specifies the time range for log query and analysis. Make sure the SQL time window follows the syntax rules of Torch Log Service (TLS). This topic describes the corresponding syntax rules and expression examples for common scenarios.

<span id="语法格式"></span>
## Syntax format

The following table describes the syntax formats supported by the SQL time window syntax.


|Format |Description |
|---|---|
|@ |Round the original time down.<br><br>For example, @h means to round the original time down to the nearest hour. If the original time is 01:23:17, the rounded time is 01:00:00. |
|+{num} |Add a specified time period to the original time.<br><br>For example, +3h means a delay of 3 hours. |
|\-{num} |Subtract a specified time period from the original time.<br><br>For example, \-30s means 30 seconds ahead. |


The following table describes the parameters.


|Parameter |Description |
|---|---|
| |Specify a positive integer. It can be omitted. The default value is 1. For example, if the time expression is `-h`, one hour is subtracted. |
| |Specify a time unit. Valid values include m, h, and d. For more information on supported time units, refer to [Time units](https://docs.byteplus.com/docs/tls/sql_time_window_syntax#%E6%97%B6%E9%97%B4%E5%8D%95%E4%BD%8D). |


<span id="时间单位"></span>
## Time units

The following table describes the time units supported by SQL time window expressions.


|**Time Unit** |**Description** |
|---|---|
|h |This unit indicates hours. |
|m |This unit indicates minutes. |
|s |This unit indicates seconds. |


<span id="表达式示例"></span>
## Expression examples

The following table describes SQL time window expressions for common scenarios.


|Start Time |End Time |**Description** |
|---|---|---|
|@m\-15m |@m |Specify that data within 15 minutes before the scheduling time is analyzed.<br><br>Assume that the start time of scheduling is 10:00, the scheduling interval is 15 minutes, the SQL time window is [@m\-15m,@m), and the execution latency is 30 seconds. In this case, the instance scheduling time is 10:00:00, the execution time is 10:00:30, and the data during the period [09:45~10:00) is analyzed. |
|@h\-3h |@h |Specify that data within 3 hours before the scheduling time is analyzed.<br><br>Assume that the start time of scheduling is 10:00, the scheduling interval is 3 hours, the SQL time window is [@h\-3h,@h), and the execution latency is 30 seconds. In this case, the instance scheduling time is 10:00:00, the execution time is 10:00:30, and the data during the period [07:00~10:00) is analyzed. |
|@h\-12h\-30m |@h |Specify that data within 12 and a half hours before the scheduling time is analyzed.<br><br>Assume that the start time of scheduling is 22:30:00, the scheduling interval is 12.5 hours (750 minutes), the SQL time window is [@h\-12h\-30m,@h), and the execution latency is 30 seconds. In this case, the instance scheduling time is 22:30:00, the execution time is 22:30:30, and the data during the period [10:00–22:30) is analyzed. |

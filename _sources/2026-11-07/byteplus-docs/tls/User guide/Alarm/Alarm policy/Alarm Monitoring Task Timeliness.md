---
title: "Alarm Monitoring Task Timeliness"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Alarm_Monitoring_Task_Timeliness"
---

The log service alarm monitoring task triggers alarms based on query and analysis results, involving the query time range and the execution time of the monitoring task. Proper time configuration improves the timeliness of the monitoring task, avoiding missed or false alarms. This article explains the timeliness of alarm monitoring tasks and provides time configuration recommendations.

<span id="85b9bcf3"></span>
## Timeliness Explanation

There is a slight delay between log writing and query or index building, which can cause missed or false alarms. Details are as follows:


* Delay Exists Between Log Writing and Querying

   There is a delay from writing logs to the log topic until the logs are queried. Although this delay is minimal, it can still cause logs to be missed in queries. Therefore, when creating an alarm policy, it is not recommended to set the **query time range** and **execution cycle** to the same relative time. For example, if the **execution cycle** is set to run every 1 minute and the **query time range** covers the last minute, then for an alarm monitoring task executing at `10:30:30`, the corresponding query time range will be `[10:29:30,10:30:30]`. Due to the delay, logs written at `10:30:29` might not be included in the query during the `10:30:30` task execution, possibly causing alarm errors.

* Low latency in index construction

   The construction of log indexes has low latency. When you write logs with different seconds in the same minute, the index data of the later logs may be saved with an earlier timestamp. For example, if the **execution cycle** is set to run every 1 minute, and the **query time range** covers the last minute, an alarm monitoring task executed at `10:30:30` will query the time range `[10:29:30, 10:30:30]`. If you write multiple logs at `10:29:40` with timestamps like `10:29:20` and `10:29:40`, their index data may be saved at `10:29:20`. Therefore, these logs won't be found in the query at `10:30:30`, which may cause alarm inaccuracies.


<span id="b082c2b8"></span>
## Time configuration recommendations

Assuming the execution cycle runs every 1 minute, configure a reasonable query time range for different scenarios.


* For high accuracy requirements where repeated or missed alarms are unacceptable,

   it is recommended to shift the query time range backward by 1 minute, such as from 2 minutes ago to 1 minute ago. For example, if the alarm monitoring task runs at `10:30:30`, the query time range should be `[10:28:30, 10:29:30]`.

* For high real\-time alarm requirements where immediate triggering is expected but repeated alarms are allowed.

   It is recommended to move the start time of the query time range 1 minute earlier to expand the query time range, such as from 2 minutes ago to 0 minutes ago. For example, if the execution time of the alarm monitoring task is `10:30:30`, the query time range is `[10:28:30, 10:30:30]`.

&nbsp;

---
title: "How scheduled SQL works"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/how_scheduled_sql_works"
---

This topic describes the implementation process, scheduling examples, and terms of scheduled SQL tasks.

<span id="implementation-process"></span>
## Implementation process

Feature implementation process:


1. When you create a scheduled SQL task, you are required to set **basic configurations** and configurations for **SQL rules**.

2. The back\-end service creates scheduled instances based on the configured task time and scheduling cycle, and performs instance scheduling on time.

   Up to one instance can be running in a task. Assume that: 1. A previous instance is delayed running because the system does not write all data within the query time range. 2. The scheduling time for the current instance is reached and the system already writes all data within the query time range. In this case, the current instance runs in priority.

   If a topic contains log data written after the end of the query time range, it means all the data within the query time range is already written. Assume that the query time range is [10:00\-11:00). If a log entry is written at 11:01, it means all the data within the query time range is already written.

3. The instance queries and analyzes a specified topic based on a configured query statement, and writes the query results to a specified topic.


<span id="sample-scheduling"></span>
## Sample scheduling

For example, when you create a task, you set the scheduling cycle to 1 hour, the SQL time window to [@h\-1h,@h), execution latency to 30 seconds, the start time of scheduling to 10:00:00 on August 17, 2023. Then, for the first instance, the scheduling time is 11:00:00, the execution time is 11:00:30, and the time range for log data query is [10:00,11:00).

<span id="terms"></span>
## Terms


|Term |Description |
|---|---|
|Scheduled SQL task |It is a collection of scheduled SQL rules. It includes basic configurations and SQL rule configurations. The former configurations include source and target topics while the latter configurations include scheduling cycles and SQL time windows. |
|Instance |After a scheduled SQL task is started, Torch Log Service (TLS) creates instances according to a specified scheduling cycle. Each instance performs scheduled SQL analysis once on the source topic and writes the calculation results to the specified topic.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">A task can generate multiple instances, but only one instance can simultaneously run in the task.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After an instance is created, the back\-end service verifies whether the instance meets the execution conditions. Instances that do not meet the conditions cannot execute analysis. For more information, refer to <a href="https://docs.byteplus.com/docs/tls/troubleshooting_query_and_analysis#%E4%B8%BA%E4%BB%80%E4%B9%88%E5%AE%9A%E6%97%B6-sql-%E4%BB%BB%E5%8A%A1%E7%9A%84%E8%B0%83%E5%BA%A6%E5%AE%9E%E4%BE%8B%E4%B8%80%E7%9B%B4%E4%B8%8D%E6%89%A7%E8%A1%8C%EF%BC%9F">Why is the instance of a scheduled SQL task not executed?</a></div><br> |
|Scheduling cycle |It is the cycle based on which a scheduled SQL task performs scheduling. The scheduling cycle determines the scheduling time of each instance. |
|Scheduling time |It is the time when a scheduled instance starts execution in a default situation. The time is determined by the scheduling cycle. The time is not affected when the previous instance has latency, encounters a timeout, or runs historical data in a supplementary manner.<br><br>If the scheduled instance does not meet the execution conditions at this point in time or execution latency is set, the time when the instance starts execution is delayed. |
|Execution time |It is the time when the instance of a scheduled SQL task actually starts execution. By default, an instance runs according to the scheduling time. If execution latency is set or the execution conditions are not met, the execution time is later than the scheduling time. For example, if the previous instance does not complete execution, the execution time is later than the scheduling time. |
|SQL time window |It is the time range for log query and analysis used when the scheduled SQL task is running. It is an left\-closed and right\-open range. After a SQL time window is specified, TLS initiates scheduled SQL tasks according to a specified scheduling cycle and analyzes the log data within a specified SQL time window. |
|Execution latency |The latency for each scheduling operation. When a collection task is busy due to a large data amount, latency may exist when the system writes data to your topic. In this scenario, you can specify execution latency to ensure data integrity during query and analysis. |

---
title: "Log query"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Log_monitoring"
---

Log query is the platform's feature for viewing and analyzing collected logs, mainly providing the following methods: log list, log search, and single trace log.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Application logs require the application to integrate Trace capability.

* Non\-application logs require configuring the Agent to collect logs from operating system files.

* Single trace logs require the application to integrate Trace capability and enable log collection capability.


<span id=".5pel5b-X6IGa57G7"></span>
## Log aggregation

Filter data by workspace, time range, tag, and parameters for each log information dimension, and display a bar chart showing log counts for different time periods.


* After you check **Auto Refresh**, the system will automatically refresh the log aggregation chart and log list according to the refresh interval.

* Supports full\-text search. The log aggregation chart and log list will display search results that meet the criteria.


<span id=".5pel5b-X5YiX6KGo"></span>
## Log list

The platform provides search capability for collected logs. Supports full\-text search; also supports filtering by log level, file line count, host name, Trace ID, and other dimensions.


* Click the **host name** in the log to go to the host monitoring details page, where you can view metrics such as the current host's CPU, load, and memory. For detailed host monitoring information, see [host monitoring](https://docs.byteplus.com/en/docs/apmplus/Basic_monitoring#.5Li75py66K-m5oOF).

* Click the **Trace ID** in the log to search for log information across the entire trace based on the current Trace ID.

* Click **Details** at the end of the log to view the complete content of the current log.

* Click **Export** at the end of the log to export the current log to your local machine in `txt` format.


<span id=".5Y2V6ZO-6Lev5pel5b-X"></span>
## Single trace log

Click the Trace ID of a log entry in the log list to search for log information across the entire trace based on the current Trace ID. To learn more about Trace Analysis, see [single trace search](https://docs.byteplus.com/en/docs/apmplus/Trace_analysis).


* Under the **Trace details** tab, you can view information about all spans in the trace, as well as associated log information, with three display options: flame graph, topology map, and list.

* Under the **Trace完整日志** tab, you can view all relevant logs for all services along the request path in a timeline, including both normal logs and error logs, which helps troubleshoot specific issues.

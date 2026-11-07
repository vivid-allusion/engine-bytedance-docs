---
title: "Report self-monitoring"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/report_self-monitoring"
---

If you have reported data but the data is not displayed on the platform, you can use the report self\-monitoring feature to perform self\-check and self\-repair.

<span id="427b3ff7"></span>
## error statistic

<span id="f36d54dd"></span>
### Filter criteria

You can filter data using the following criteria:

time, data type, environment, error level, error category, error message, error location.

<span id="c2cc1b92"></span>
### Error data


* Filter fields: Displays all filterable fields. Click to expand a field to display a dropdown list of selectable values for each field.

* Detection results: Displays the aggregated results of reported error logs, including error count, trends, logs, and error locations. By default, items are sorted in descending order by the number of logs, and pagination is supported.

   * For each category of error log, click '+'' to expand and display each log in that category. Logs are sorted in reverse order by error occurrence time, and pagination is supported.

      Only one log is reported for the same type of error within 30 seconds. Therefore, when you expand the logs, you may find that the number of logs does not match the error count. This may be because the same type of error occurred repeatedly within 30 seconds, and the platform only sampled and obtained one log.

   * Trend: When you hover over with your mouse, you can view the specific time and error count.

   * Log: Click **show more** to view additional error logs to help analyze data.

   * payload: Click **payload** to locate the error location in the log.

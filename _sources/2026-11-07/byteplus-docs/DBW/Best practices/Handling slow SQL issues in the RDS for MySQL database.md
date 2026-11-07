---
title: "Handling slow SQL issues in the RDS for MySQL database"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/troubleshooting-slow-sql-log-issues-of-mysql-databases"
---

During RDS for MySQL troubleshooting, abnormal performance indicators such as high database CPU utilization, long response times, and high IO consumption may be caused by slow SQL. Therefore, when troubleshooting RDS for MySQL database failures, checking slow SQL is a common and effective method. Slow SQL analysis can help you quickly locate database problems and propose corresponding optimization measures. This topic describes how to handle slow SQL issues in the RDS for MySQL database through the slow SQL analysis function.

<span id=".6YCa6L-H5oWiLXNxbC3liIbmnpDmjpLmn6UtbXlzcWwt5pWF6Zqc"></span>
## Troubleshoot RDS for MySQL failures through slow SQL analysis

The slow SQL analysis function can not only help you quickly view the development trend, statistics, and details of slow SQL in an instance or read\-only nodes within an instance, but also further analyze the slow SQL information and provide SQL optimization suggestions to help you fast locate database problems. For more information, refer to [Slow log analysis](https://docs.byteplus.com/en/docs/DBW/slow-log-analysis-management-for-PG?type=preview&lang=en) and [Slow log management](https://docs.byteplus.com/en/docs/DBW/slow-log-analysis-management-for-PG?type=preview&lang=en).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can also view the overall database performance through the one\-click diagnosis function to quickly confirm whether there are any anomalies in the database. For more information on one\-click diagnosis, refer to <a href="https://docs.byteplus.com/en/docs/DBW/one-click-diagnostics-management-for-mysql?type=preview&lang=en">One\-click diagnosis management</a>.</div>

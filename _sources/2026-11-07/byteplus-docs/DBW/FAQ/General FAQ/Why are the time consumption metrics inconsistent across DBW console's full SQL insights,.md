---
title: "Why are the time consumption metrics inconsistent across DBW console's full SQL insights, audit logs, and slow logs?"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/what-to-do-when-system-reports-session-create-failed-log-in-instance-on-data-interaction-platform"
---

This inconsistency arises because the time collection methods differ for `ThreadScheduleTime` in full SQL insights, execution time in audit logs, and total time (s) in slow log analysis, as detailed below:


* Full SQL Insights: The `ThreadScheduleTime` in full SQL insights collects runtime (RT) at the kernel level.

* Audit Logs: The execution time in audit logs collects the response time (RT) in the public service network.

* Slow Log Analysis: The total time (s) in slow log analysis collects the execution time of the statement.

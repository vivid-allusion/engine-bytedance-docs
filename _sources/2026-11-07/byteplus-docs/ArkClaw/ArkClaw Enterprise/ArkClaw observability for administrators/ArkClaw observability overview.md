---
title: "ArkClaw observability overview"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/ArkClaw_observability_overview"
---

ArkClaw instance anomalies found in operations and maintenance (O&M) often manifest across multiple dimensions. Isolated log queries or metric monitoring rarely capture the full context of anomalies. The ArkClaw observability module integrates these fragmented observability entry points into a unified system, providing administrators with full lifecycle ArkClaw observability capabilities. These capabilities cover core scenarios, including alert configuration, real\-time monitoring, performance and trace diagnosis, log analysis, and operational auditing, forming an end\-to\-end closed O&M loop from risk detection to responsibility tracing.

<span id="yF7pXbRD"></span>
## Observability system

ArkClaw observability provides a comprehensive O&M observability loop that spans three stages: pre\-event monitoring, in\-event troubleshooting, and post\-event tracing.


* **Pre\-event monitoring**: This stage corresponds to "continuous awareness" and "proactive prevention". Before anomalies occur, risks are proactively identified using alert rules and monitoring dashboards. This stage focuses on capturing key metrics, instance status, and risk signals into the observability system before they impact services. Administrators detect issues early via automated alerts and routine inspections.

* **In\-event troubleshooting**: This stage corresponds to "rapid root\-cause identification" and "progressive drill\-down". When anomalies occur, leverage multidimensional analysis across usage metrics, performance, sessions, traces, logs, and other information to facilitate root cause identification. When an anomaly is detected via alerts or inspections, perform synchronous evidence collection across dimensions, including usage, performance, sessions, traces, and logs, to pinpoint root causes with minimal steps.

* **Post\-event tracing**: This stage corresponds to "evidence traceability" and "governance review". After anomaly resolution, conduct reviews and compliance governance by using configuration change records and audit logs. After issues are identified and resolved, confirm whether they are related to configuration changes or critical operations to support subsequent optimization, auditing, and responsibility attribution.


<span id="nGQZtACa"></span>
## Feature overview


|Stage |Feature module |Description |<div style="text-align: center"><br>Employee Claw</div><br> |<div style="text-align: center"><br>Enterprise service agent</div><br> |
|---|---|---|---|---|
|Pre\-event monitoring |[Creating ArkClaw alert tasks](https://docs.byteplus.com/en/docs/ArkClaw/Creating_ArkClaw_alerting_tasks) |Configure alert rules for key ArkClaw metrics and establish automatic alert triggers via notification policies. When abnormal fluctuations occur in key metrics, the responsible personnel will be notified automatically to reduce issue detection time. |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>✅</div><br> |
||[Viewing ArkClaw instance dashboards](https://docs.byteplus.com/en/docs/ArkClaw/Viewing_the_monitoring_dashboard_for_an_ArkClaw_instance) |Inspect task executions, token consumption, skill access, tool invocation, and anomaly distribution to monitor the status of a specific ArkClaw instance, including its resource consumption and operational performance. This enables proactive identification of abnormal consumption and load trends at an early stage. |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>❌</div><br> |
|In\-event troubleshooting |[Viewing ArkClaw usage data](https://docs.byteplus.com/en/docs/ArkClaw/Viewing_ArkClaw_usage_data) |Monitor active instances, token consumption, cache hit rates, and usage rankings globally to gain real\-time insights into ArkClaw's resource consumption. This provides quick access to resource consumption changes, capacity pressure, and resource instance distribution during anomaly handling. |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>✅</div><br> |
||[Viewing ArkClaw performance data](https://docs.byteplus.com/en/docs/ArkClaw/Viewing_ArkClaw_performance_data) |Analyze overall performance status from the perspectives of request volume, latency, and resource usage. This can be used to troubleshoot performance degradation, resource bottlenecks, and abnormal system loads. |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>✅</div><br> |
||[Viewing ArkClaw session data](https://docs.byteplus.com/en/docs/ArkClaw/Viewing_ArkClaw_sessions) |Track the complete interaction process of ArkClaw during a specific time period to restore the user interaction context from the session dimension and reproduce the issue scenarios. This information can be used to diagnose abnormal responses, missing context, or session execution failures. |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>✅</div><br> |
||[Viewing ArkClaw traces](https://docs.byteplus.com/en/docs/ArkClaw/Viewing_ArkClaw_traces) |Track and view ArkClaw's complete traces and spans along the call paths to identify latency points, failed traces, and dependency issues. This information can be used for locating timeouts, failed calls, and upstream/downstream anomalies. |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>✅</div><br> |
||[Viewing ArkClaw log statistics](https://docs.byteplus.com/en/docs/ArkClaw/Viewing_ArkClaw_log_statistics) |Provide statistics on total log volume, error log scale, and rankings of abnormal instances to detect sudden surges in error logs or aggregation of abnormal instances. |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>✅</div><br> |
||[Viewing ArkClaw log analysis](https://docs.byteplus.com/en/docs/ArkClaw/Viewing_ArkClaw_log_analysis) |Troubleshoot issues based on keywords and extract raw evidence. Perform visual queries on ArkClaw logs and conduct in\-depth log analysis to facilitate quick root cause analysis and system performance monitoring. |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>✅</div><br> |
|Post\-operation traceability |[Viewing ArkClaw audit logs](https://docs.byteplus.com/en/docs/ArkClaw/Viewing_ArkClaw_audit_logs) |View records of critical operations and events during ArkClaw usage. Event and responsibility tracing is supported. This information can be used to confirm the operator, operation time, and results of critical operations. |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>❌</div><br> |
||[Viewing ArkClaw configuration change records](https://docs.byteplus.com/en/docs/ArkClaw/Viewing_the_configuration_modification_records_for_an_ArkClaw_instance) |View the change history and detailed additions, deletions, and updates of the `openclaw.json` file to determine whether a failure is triggered by configuration changes, and identify the operator and change time. |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>❌</div><br> |

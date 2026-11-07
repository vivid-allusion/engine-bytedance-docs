---
title: "Viewing monitoring information"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_monitoring_information"
---

This topic describes how to view monitoring information.

<span id=".55uR5o6n5L-h5oGv6K-05piO"></span>
## Monitoring data collection

Cloud Monitoring supports selecting different query time ranges, aggregation cycles, and aggregation methods to process and display monitoring data.

Cloud Monitoring supports query time ranges from 1 minute to 30 days.

Cloud Monitoring supports aggregation cycles of 5 seconds, 30 seconds, 1 minute, 5 minutes, 10 minutes, 30 minutes, 1 hour, 3 hours, 6 hours, and 24 hours. The frequency of monitoring data collection varies with the aggregation cycle. When the aggregation cycle is 5 seconds, Cloud Monitoring collects data every 5 seconds. When the aggregation cycle is 30 seconds, 1 minute, 5 minutes, 10 minutes, 30 minutes, 1 hour, 3 hours, 6 hours, or 24 hours, Cloud Monitoring collects data every 30 seconds.

Cloud Monitoring supports five aggregation methods: default value, average value, maximum value, minimum value, and sum. These methods are described as follows:


* **Default value**: The value obtained directly from a query expression for a metric.

* **Average value**: The average of the original values within a statistical period.

* **Maximum value**: The largest of the original values within a statistical period.

* **Minimum value**: The smallest of the original values within a statistical period.

* **Sum value**: The sum of the original values within a statistical period.


The supported aggregation periods vary for different query time ranges, and the supported aggregation methods also vary for different aggregation periods, as shown in the table below.


|**Query time range** |**Supported aggregation cycle** |**Supported aggregation methods** |
|---|---|---|
|(0~1] hours<br><br> |5 seconds |Default value |
||30 seconds ||
||1 minute |Default value, Average value, Maximum value, Minimum value, Sum<br><br> |
||5 minutes ||
||10 minutes ||
||30 minutes ||
|(1~6] hours |30 seconds |Default value |
||1 minute |Default value, average value, maximum value, minimum value, sum value<br><br> |
||5 minutes ||
||10 minutes ||
||30 minutes ||
|(6~24] hours |1 minute |Default value, average value, maximum value, minimum value, sum value |
||5 minutes ||
||10 minutes ||
||30 minutes ||
||1 hour ||
|(1\-3] days |10 minutes |Default value, average value, maximum value, minimum value, sum value<br><br> |
||30 minutes ||
||1 hour ||
||3 hours ||
||6 hours ||
|(3~7] days |10 minutes |Default value |
|(7~15] days |1 hour |Default value |
|(15~30] days |24 hours |Default value |


Monitoring data with an aggregation period of 5 or 30 seconds is retained for 1 day. Monitoring data with an aggregation period of 1 minute, 5 minutes, 10 minutes, 30 minutes, 1 hour, 3 hours, 6 hours, or 24 hours is retained for 30 days.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Monitoring data aggregation period The values of the same monitoring item at the same time point slightly differ under different aggregation periods. To view accurate values, select a smaller time range.</div>


* <div data-tips="true" data-tips-type="tip">For instances of MySQL 8.4.7_20260415, MySQL 8.0.43_20251015,  MySQL 5.7.44_20251015, and later versions, RDS for MySQL provides 5\-second monitoring for some monitoring items. For a list of supported items, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/monitoring_metrics#.5a6e5L6LLeiKgueCueWPjOe7tOW6puebkeaOp-mhueWIl-ihqA==">List of monitoring items that support multi\-dimensional viewing</a>. This feature is currently in beta testing by invitation only. To use it for free, apply by <a href="https://console.byteplus.com/workorder/create/">submitting a ticket</a>. If this capability is charged in the future, RDS for MySQL will announce the billing details one month in advance.</div>



<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.</div>



3. Click on **Instances** in the left navigation bar.

4. On the **Instances** page, click on the target instance name.

5. Click on the **Monitoring** tab at the top of the page.

6. Click on the **Monitoring** tab to view **Resource monitor**, **Engine monitor**, **Deployment monitor**, and **Proxy monitor** details of the instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Resource Monitoring, Deployment Monitoring, and Engine Monitoring allow you to view various monitoring metrics by node. On the <strong>Resource Monitoring</strong>, <strong>Deployment Monitoring</strong>, and <strong>Engine Monitoring</strong> pages, you can select a Node ID on the left to view the monitoring metric data for the primary node, standby node, and read\-only nodes respectively, or select All nodes to view the monitoring data for all nodes.</div>


* <div data-tips="true" data-tips-type="tip">Database Proxy Monitoring only supports viewing monitoring metrics by instance.</div>


* <div data-tips="true" data-tips-type="tip">For descriptions of monitoring metrics, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/monitoring_metrics">Monitoring metrics</a>. You can also click <strong>View more metrics</strong> on the right to view the <strong>Alert Overview</strong> of the instance, or click <strong>Create Alert Rule</strong> to create a new <strong>alert policy</strong> for the instance. For more details, refer to <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy">Creating alert policies</a>.</div>


* <div data-tips="true" data-tips-type="tip">You can customize the time range to view, down to the minute. RDS for MySQL also provides quick options: Recent 10 minutes, Recent 1 hour, Recent 3 hours, Recent 6 hours, Recent 12 hours, Recent 1 day, Recent 3 days, and Recent 7 days. You can view monitoring data for up to 30 days.</div>


* <div data-tips="true" data-tips-type="tip">After you select <strong>Chart Linkage</strong>, you can quickly view the monitoring metrics and their values at the same point in time across all charts.</div>


* <div data-tips="true" data-tips-type="tip">When the database proxy feature is not enabled for the instance, the <strong>Proxy monitoring</strong> page is not available. When the database proxy is enabled, you can view the proxy monitoring page and check monitoring information by instance and Endpoint.</div>

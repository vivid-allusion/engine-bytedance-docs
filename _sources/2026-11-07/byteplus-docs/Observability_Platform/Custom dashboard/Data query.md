---
title: "Data query"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Data_query"
---

Custom dashboards support multiple data sources, including Server\-side Monitoring, VMP, Cloud Monitor, TLS, MySQL, and Metrics. This topic describes how to configure data queries by data source.

> **tip**

> The data query feature allows you to add multiple query statements. You can copy, hide, or delete individual statements. When a statement is hidden, its configurations are retained but do not take effect.

## Application performance monitoring (server side)

After specifying "Server\-side Monitoring \- server side" as the data source, you need to select a region and workspace. Two query methods are available for configuring data queries: semantic query and PromQL. After selecting semantic query, you can select a metric name, specify aggregation dimensions, and add filters to filter the query results.

The default Format option is the time series format, which can be used for time series diagrams and metric cards. If you choose table\-based visualization, we recommend setting Format to the table format.

> **tip**

> Custom dashboards can be associated with custom tags configured for ArkClaw instances. When configuring a custom dashboard, you can use ArkClaw instance custom tags in filter conditions to filter data and in GroupBy to query data by group. For details of ArkClaw instance custom tags, see [Managing tags](https://docs.byteplus.com/en/docs/ArkClaw/Tag_management).

## Vital Managed Service for Prometheus

When VMP is used as the data source, you need to select a region and workspace, and enter the PromQL statement in the query field to query metric data.

By configuring Legend, you can format a time series diagram and use `{{LabelName}}` syntax for label variable replacement. The default Format option is the time series diagram format, which can be used for time series diagrams and metric cards. If you choose table\-based visualization, we recommend setting Format to the table format. The "real time" toggle is disabled by default. When enabled, only real\-time data will be retrieved.

## Cloud Monitor

When Cloud Monitor is used as the data source, you need to specify the Namespace, Region, and SubNamespace for filtering the target data. Then, select a specific metric to be queried via the Metric Name field.

You can check the "Whether to select all resources" option to select all resources. When this option is not selected, you can filter resources by project and resource type.

|Parameters |Description |
|---|---|
|Namespace |The product namespace to which the target metric belongs. For details, see the Namespace of each product in [Cloud product monitoring metrics](https://console-stable.volcanicengine.com/cloud_monitor/metricDoc?tabKey=metric). |
|region |The region list is populated automatically based on the selected Namespace value. Click to select a region. |
|MetricName |The name of the metric to be queried. For details, see the MetricName of each product in [Cloud product monitoring metrics](https://console-stable.volcanicengine.com/cloud_monitor/metricDoc?tabKey=metric). |
|SubNamespace |The dimension to which the metric to be queried belongs. The supported values of SubNamespace differ by Namespace. For details, see the SubNamespace of each product in [Cloud product monitoring metrics](https://console-stable.volcanicengine.com/cloud_monitor/metricDoc?tabKey=metric). |
|projectName |The project to which the monitoring product resource to be queried belongs. |
|Resource |The category of the monitoring product resource to be queried. |
|Resource name |The monitoring resource to be queried. The field is populated based on the values of Namespace, Region, and Resource automatically. Click to select a resource. |
|Period |The interval granularity for data to be queried. Seconds (s), minutes (m), hours (h), days (d), and weeks (w) are supported.<br><br>For example, after you query data within 10 minutes with a 1\-minute interval, 10 data points will be returned. When the selected time range is long, it is not recommended to use a small interval. Otherwise, the dataset may be excessively large.<br><br>> **tip**<br><br><br>> For details on how Period affects the offset of StartTime and EndTime, .<br> |
|GroupBy |The grouping dimension of the metric to be queried. By default, all dimensions are used for metric grouping. When optional dimensions are available for a metric, specify the Group By parameter to select a specific optional dimension. . |

## Torch Log Service (TLS)

When TLS is used as the data source, you need to select a region and a log topic for filtering the target data. Then, enter the search analysis statement to query the metric. By default, data from all fields is queried. You can filter the query range by field. Separate multiple fields with commas.

The default Format option is the time series diagram format, which can be used for time series diagrams and metric cards. If you choose table\-based visualization, we recommend setting Format to the table format.

## Metrics

When Metrics is used as the data source, metric data can be queried via OpenTSDB and InfluxDB protocols. During configuration, regardless of which protocol is used, first select the region and workspace. In addition, the InfluxDB protocol supports semantic query and InfluxQL configuration modes, and the OpenTSDB supports queries based on a combination of metrics and filters.

## MySQL

When MySQL is used as the data source, you can query detailed data and aggregated data in MySQL databases. Before you begin, you need to configure the MySQL data source in [Data source management](https://docs.byteplus.com/en/docs/observability/data-source-management) and ensure network connectivity between the platform server and the database. When querying data, you can use Builder mode to visually select data tables, fields, and filters, or use Code mode to write SQL statements. Query results can be returned in Table or Time series format, which you can use to display detailed data and analyze trends, respectively.

---
title: "Product features"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Product-features"
---

<span id="kNmp6UJW"></span>
## workspace


|Feature |Description |
|---|---|
|workspace |A VMP workspace is an abstract integration of data and collection rules, which provides you with standard Prometheus capabilities on the cloud. You can create, update, and delete workspaces. |
|Authentication Method |The workspace supports two authentication methods:  AK/SK and Basic Auth. |
|Read and write address |VMP provides independent remote write URLs, query URLs, push gateway URLs, and federated query URLs that can be accessed over internal networks for reading and writing the data of workspaces. |
|Recording rule |* You can create recording rules to perform secondary aggregation of data. This reduces resource usage on the query side and improves query efficiency.<br><br>* You can configure recording rules by using YAML rule files. You can filter data by using standard PromQL statements.<br><br>* You can view, export, edit, and delete recording rule files. |
|Workspace monitoring |VMP provides the self\-monitoring capabilities of workspaces and allows you to view the trends of write, query, and storage metrics of workspaces within a specified time range. This helps you identify issues such as rate limiting and invalid metrics during self\-troubleshooting. |


<span id="rUMGEMUX"></span>
## Integration center


|Feature |Description |
|---|---|
|Cloud service integration |VMP can be used to monitor the metrics, operational status, and resource usage of cloud native services of  and generate related alerts. The integrated services include Vital Kubernetes Engine (VKE), ECS, Cloud Monitor, Microservices Engine (MSE), API Gateway (APIG), and other services. |
|Self\-built Kubernetes cluster integration |VMP provides the native Prometheus collection solution and the high\-availability collection solution to help you integrate your self\-built Kubernetes cluster. |
|Custom business integration |You can use the various SDKs provided by the open source community to define business metrics during application development, and then monitor the applications or services by using VMP. |
|Exporter integration |Various exporters are provided by the open source community to monitor various environments, middleware, and custom applications. |


<span id="5XrKYt0M"></span>
## Resource consumption

The "Resource Consumption" page allows you to view resource consumption statistics for all Standard workspaces within the current account, including basic metrics and other & custom metrics. This helps you understand the distribution of the metrics in the system.


|Feature |Description |
|---|---|
|Metric consumption statistics |Summarizes the reported and written volumes of basic metrics, other metrics, and custom metrics. Cumulative data for the past 24 hours and the past 14 days are provided for you to quickly assess the consumption scale. |
|Metric reporting trend |Displays the trend of changes in the reported volumes by type, with support for Min, Max, and Avg statistics. This information is used to observe fluctuations in data collection volume and assist with anomaly investigation. |
|Metric write trend |Displays the trend of written volume changes by type, with support for Min, Max, and Avg statistics. This information is used to analyze the data write volume and assist with cost analysis and governance. |
|Metric ranking analysis |You can view the rankings of metrics by workspace, metric, and job. You can understand the distribution of the metric sample volume in the system and adjust metric collection rules accordingly. |


<span id="Bz89FSDF"></span>
## Explore


|Feature |Description |
|---|---|
|Metrics queries |* The Explore feature allows you to query collected metric information by using standard PromQL statements.<br><br>* The metric preview images can be dynamically refreshed through manual refresh or scheduled refresh.<br><br>* You can configure query metrics. You can enter PromQL query statements or select the target metric, label, and value from the lists to filter data.<br><br>* You can use the historical query feature. The system automatically records used query statements and provides a historical query list. This helps you quickly obtain historical query statements. |


<span id=".5ZGK6K2m566h55CG"></span>
## Monitoring dashboard


|Feature |Description |
|---|---|
|Viewing dashboards |You can view preset monitoring dashboards, which centrally display key monitoring data for services or scenarios. |
|Metric overview |Displays current values and trends of key metrics (for example, CPU and GPU) using statistic cards and trend charts. |


<span id="32PsPs0s"></span>
## Alert Center


|Feature |Description |
|---|---|
|Contacts |* You can configure alerting contacts.<br><br>* You can configure alerting contact groups. You can add specified contacts to contact groups. |
|Alerting notification channel |VMP supports multiple types of alerting notification channels, including:<br><br><br>* Email<br><br>* Phone call<br><br>* Generic webhook<br><br>* Feishu bot<br><br>* Feishu application robot<br><br>* DingTalkBot<br><br>* WeCom robot |
|Alert rules |* You can configure alert rules by using specified workspaces and PromQL statements to monitor specific resources.<br><br>* You can configure alerting trigger policies to classify alerts based on different thresholds and durations (P0, P1, and P2).<br><br>* You can associate alert notification policies with alerting aggregation policies in alert rules. |
|Alerting rule template |* The system presets alert rule templates for commonly used cloud services to help you quickly create alert rules.<br><br>* You can create custom alerting rule templates by using the console or YAML files. |
|Alert notification policy |You can configure alerting notification policies. You can configure notification recipients and methods for alerts at different levels (P0, P1, and P2). |
|Notification template |You can configure notification templates, which allow you to use Markdown syntax and Go Template syntax to specify custom notifications. |
|Alert aggregation strategy |You can configure alerting aggregation policies to specify the alerting aggregation interval and notification interval. This minimizes alert storms. |
|Alerting silence policies |You can configure alert silence policies to block alert notifications when the alerts cannot be resolved. |
|View alerts |* You can view the current alert list in the system. The information about alerts includes alert ID, current status, alert level, workspace, alert resource, occurrence time, and associated rules.<br><br>* You can view alert details. The details include current alert information, alert metrics, and alert status transitions. |


<span id=".6ZuG5oiQ5Lit5b-D"></span>
## Export tasks


|**Feature** |**Description** |
|---|---|
|Create tasks |You can configure data filter conditions and query offsets, and select an export destination (Message Queue for Kafka, self\-managed Prometheus, or TOS) to control the export scope and delivery method as needed. |
|Task query |You can filter for tasks by workspace and task name to quickly locate the target task. |
|Task management |Displays the task name, export destination, status, labels, and workspace so that you can view task information in one place. |
|Task operations |You can edit, pause, or delete tasks to adjust or stop exports as needed. |


&nbsp;

&nbsp;

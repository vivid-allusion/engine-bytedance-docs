---
title: "Change log of Milvus metrics"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Change_announcement_on_Milvus_metrics"
---

The Cloud Monitor team will soon adjust the monitoring metrics for the Milvus vector database, aiming to provide you with a more accurate and comprehensive monitoring experience.

> **tip**

> For cloud product metrics and details, see [Cloud product metrics query](https://console.byteplus.com/cloud_monitor/docs).

## 2026\-11

|MetricName |SubNamespace |Type |Description |Impact |
|---|---|---|---|---|
|StoredIndexFilesSize |collection |Unit change |The metric unit has changed from `Bits(IEC)` to<br><br>`Bytes(IEC)`. |* This change does not affect the normal operation of cloud product instances and your business.<br><br>* Monitoring dashboards will display data based on the updated metrics.<br><br>* Alert rules remain unchanged and active. Alert notifications will be sent according to the settings in alert rules. |

## October 2026

|MetricName |SubNamespace |Type |Description |Impact |
|---|---|---|---|---|
|Proxy_Memory_Usage |resource |Unit change |The metric unit has changed from `Bits(IEC)` to<br><br>`Bytes(IEC)`. |* This change does not affect the normal operation of cloud product instances and your business.<br><br>* Monitoring dashboards will display data based on the updated metrics.<br><br>* Alert rules remain unchanged and active. Alert notifications will be sent according to the settings in alert rules. |
|QueryNode_Memory_Usage |||||
|DataNode_Memory_Usage |||||
|IndexNode_Memory_Usage |||||
|MixCoord_Memory_Usage |||||
|StreamingNode_Memory_Usage |||||

## March 2026

|MetricName |SubNamespace |Type |Description |Impact |
|---|---|---|---|---|
|ReadQPS |performance |Unit change |The metric unit will change from `None` to `Count/Second`. |* This change does not affect the normal operation of cloud product instances and your business.<br><br>* Monitoring dashboards will display data based on the updated metrics.<br><br>* Alert rules remain unchanged and active. Alert notifications will be sent according to the settings in alert rules. |
|ReadVPS |||||
|WriteQPS |||||
|InsertVPS |||||
|UpsertVPS |||||
|DeleteVP |||||

## February 2026

|MetricName |SubNamespace |Type |Description |Impact |
|---|---|---|---|---|
|SearchRequestVPS |collection |Metric deprecation |\- |* This change does not affect the normal operation of cloud product instances and your business.<br><br>* Related charts disappear from the monitoring dashboard, and you cannot specify the corresponding metrics during queries.<br><br>* If an exclamation mark (!) is added before an existing alert rule, it indicates that the alert rule contains a deprecated metric, and the alert will no longer be triggered. You need to remove the deprecated metric from the alert rule.<br><br>* If you do not remove or update the deprecated metric for an existing alert template, you cannot save the template.<br><br>* If you configured this metric in a [custom dashboard using the Grafana add-on](https://docs.byteplus.com/en/docs/cloudmonitor/Custom-dashboard-through-Grafana-plugin), the related monitoring data becomes unavailable.<br><br>* If you have configured this metric by using a [custom observability dashboard](https://docs.byteplus.com/en/docs/Observability_Platform/Quickly_start_using_custom_dashboards), the related monitoring data will be unavailable. |
|SearchRequestVPSV3 |||||
|QueryNodeSegmentNum |||||
|StoredBinlogSize |||||

## July 2025

|MetricName |SubNamespace |Type |Description |Impact |
|---|---|---|---|---|
|RoleNodeNumber |function |Usage deprecation |* Before the change, the usage purpose of the metric was alerting.<br><br>* After the change, the usage purpose of the metric is none. |* This change does not affect the normal operation of cloud service instances and your business.<br><br>* Monitoring dashboards can still display data based on metrics.<br><br>* If an exclamation mark (!) is added before an existing alert rule, it indicates that the alert rule contains an invalid metric, and the alert will no longer be triggered. You need to modify the metric in the alert rule.<br><br>* If you do not remove or update the metric for an existing alert template, you cannot save the template. |
|CollectionCnt |meta |Usage deprecation |* Before the change, the usage purpose of the metric was consumption.<br><br>* After the change, the usage purpose of the metric is none. |* This change does not affect the normal operation of cloud product instances and your business.<br><br>* The corresponding metric cannot be queried during cloud product metric queries.<br><br>* Metrics cannot be retrieved or exported through the Grafana plug\-in, API, or exporter, with a message indicating that the metric does not exist. |

## May 2025

|MetricName |SubNamespace |Type |Description |Impact |
|---|---|---|---|---|
|NodeNumber |resource |Usage deprecation |* Before the change, the usage purpose of the metric was alerting.<br><br>* After the change, the usage purpose of the metric is none. |* This change does not affect the normal operation of cloud service instances and your business.<br><br>* Monitoring dashboards can still display data based on metrics.<br><br>* If an exclamation mark (!) is added before an existing alert rule, it indicates that the alert rule contains an invalid metric, and the alert will no longer be triggered. You need to modify the metric in the alert rule.<br><br>* If you do not remove or update the metric for an existing alert template, you cannot save the template. |

##

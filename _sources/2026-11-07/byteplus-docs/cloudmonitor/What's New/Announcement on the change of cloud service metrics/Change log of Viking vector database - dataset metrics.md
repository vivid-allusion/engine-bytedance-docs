---
title: "Change log of Viking vector database - dataset metrics"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Change_log_on_Viking_vector_database_-_dataset_metrics"
---

The Cloud Monitor team will soon adjust the monitoring metrics for the Viking vector database \- dataset, aiming to provide you with a more accurate and comprehensive monitoring experience.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For cloud product metrics and details, see <a href="https://console.byteplus.com/cloud_monitor/docs">Cloud product metrics query</a>.</div>


<span id="4FmUWfXT"></span>
## June 2026


|MetricName |SubNamespace |Type |Description |Impact |
|---|---|---|---|---|
|CollectionSyncUpsertDataQPS |Data |Unit change |The metric unit is changed from `Count/Second` to `Count`. |* This change does not affect the normal operation of cloud product instances and your business.<br><br>* Monitoring dashboards will display data based on the updated metrics.<br><br>* Alert rules remain unchanged and active. Alert notifications will be sent based on the unit configured in the alert rules. |
|CollectionAsyncUpsertDataQPS |||||
|CollectionUpsertDataCount |||||
|CollectionDeleteDataCount |||||
|CollectionUpdateDataCount |||||
|CollectionFetchDataCount |||||


<span id="IT0QdeCq"></span>
##

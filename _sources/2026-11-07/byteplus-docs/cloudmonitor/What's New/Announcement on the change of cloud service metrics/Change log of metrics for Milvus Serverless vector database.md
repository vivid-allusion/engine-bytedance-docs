---
title: "Change log of metrics for Milvus Serverless vector database"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/announcing-milvus-server-less-for-vector-db-metric-changes"
---

The Cloud Monitor team will soon adjust metrics for the Milvus Serverless vector database to deliver comprehensive monitoring with improved precision.

> **tip**

> For cloud product metrics and details, see [Cloud product metrics query](https://console.byteplus.com/cloud_monitor/docs).

## 2026\-11

|MetricName |SubNamespace |Type |Description |Impact |
|---|---|---|---|---|
|StoredBinlogSize |collection |Unit change |The metric unit has changed from `Bits(IEC)` to<br><br>`Bytes(IEC)`. |* This change does not affect the normal operation of cloud product instances and your business.<br><br>* Monitoring dashboards will display data based on the updated metrics.<br><br>* Alert rules remain unchanged and active. Alert notifications will be sent according to the settings in alert rules. |
|StoredIndexFilesSize |||||

## March 2026

|MetricName |SubNamespace |Type |Description |Impact |
|---|---|---|---|---|
|ReadQPS |performance |Unit change |The metric unit will change from `None` to `Count/Second`. |* This change does not affect the normal operation of cloud product instances and your business.<br><br>* Monitoring dashboards will display data based on the updated metrics.<br><br>* Alert rules remain unchanged and active. Alert notifications will be sent based on the unit configured in the alert rules. |
|ReadVPS |||||
|WriteQPS |||||
|InsertVPS |||||
|UpsertVPS |||||
|DeleteVP |||||

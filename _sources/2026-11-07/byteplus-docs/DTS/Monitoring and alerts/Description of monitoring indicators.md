---
title: "Description of monitoring indicators"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/monitoring_metrics"
---

The Database Transfer Service (DTS) supports real\-time monitoring of data transfer rates, including full migration, full initialization, full validation, incremental migration, incremental synchronization, and incremental validation related transfer rates, providing performance data reference for you to manage data transfer tasks.

<span id=".55uR5o6n5oyH5qCH6K-05piO"></span>
## Description of monitoring indicators

You can call the [GetMetricData](https://docs.byteplus.com/en/docs/cloudmonitor/GetMetricData) interface to query the monitoring metrics data of the Database Transmission Service (DTS) task. When calling this interface to query, you need to obtain relevant information about the following monitoring metrics:


* **Namespace**: The product space to which the monitoring indicator to be queried belongs. The product space name of DTS is `VCM_DTS`.

* **SubNamespace**: The dimension to which the metric to query belongs. The DTS task supports monitoring metrics of the `basic_monitoring` dimension (basic dimension).

* **MetricName**: The name of the monitoring indicator to be queried. The MetricName corresponding to each monitoring indicator of the DTS task is shown in the table below. For more details, refer to the [Coud monitoring indicator query](https://console.byteplus.com/cloud_monitor/docs?namespace=VCM_DTS).


<span id=".55uR5o6n5oyH5qCH6aG5"></span>
## Monitoring metrics

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Cloud monitoring acquires data every 30 seconds by default, and displays the collected data after obtaining the average or maximum value according to the display granularity of the query results. For more information about monitoring metrics, refer to <a href="https://docs.byteplus.com/en/docs/DTS/viewing_monitoring_data">Monitoring metrics</a>.</div>


* <div data-tips="true" data-tips-type="tip">The units in the monitoring indicator table are all basic units. Please refer to the console for the specific units of each monitoring. The units displayed on the console will be flexibly adjusted based on the monitoring values following the SI standards. For example, the base unit of full transmission BPS is Byte/s. If the monitoring value of full transmission BPS is large, the unit on the console may be adjusted to KB/s, MB/s, GB/s, etc.</div>




|**Metric item** |**MetricName** |**Unit** |**Description** |
|---|---|---|---|
|Task delay |Latency |ms |The time difference between DTS fetching the latest data from the source and writing it to the target. |
|Full transmission BPS |FullTransmissionBps |Byte/s |Amount of data transmitted per second during full migration or full initialization. |
|Full transmission RPS |FullTransmissionRps |Count/s |The number of rows transmitted per second during full migration or full initialization. |
|Incremental transmission BPS |IncrementalTransmissionBps |Byte/s |The amount of data transferred per second during incremental migration or full initialization. |
|Incremental transmission RPS |IncrementalTransmissionRps |Count/s |Number of rows transmitted per second during incremental migration or full initialization. |
|Average packet loss rate at the source |PacketLossRateAvgOfSrc |% |The ratio of data packets lost in average network communication at the source to the number of packets sent. The average value is calculated based on statistics at a granularity of 30 seconds. |
|Average packet loss rate at the target |PacketLossRateAvgOfDest |% |The ratio of data packets lost in average network communication at the target to the number of packets sent. The average value is calculated based on statistics at a granularity of 30 seconds. |
|Source average delay |SrcDelayAvg |μs |The average delay from the <Source database\> to Database Transmission Service (DTS) within the specified time range. The average value is calculated based on statistics at a granularity of 30 seconds. The default unit of this metric is μs. When the next time carry is reached, the unit presentation will be automatically updated in the following order: μs, ms, s, min, h. |
|Average target delay |DestDelayAvg |μs |Within the specified time range, the average delay required for Database Transmission Service (DTS) to the target database. The average value is calculated based on statistics at a granularity of 30 seconds. The default unit of this metric is μs. When the next time carry is reached, the unit presentation will be automatically updated in the following order: μs, ms, s, min, h. |
|Source database Binlog delay |SrcBinlogDelay |ms |During data synchronization or migration for MySQL instances, the time difference between the latest Binlog fetched by DTS and the latest Binlog actually generated at the source. |
|Number of increment validation inconsistencies |IncrDiffNum |Count |Total rows of inconsistent data found during incremental validation. |
|Increment validation BPS |IncrDataValidationBPS |MB/s |The amount of data verified per second during increment validation. |
|Increment validation RPS |IncrDataValidationRPS |Count/s |Total rows of data verified per second during increment validation. |
|Full data verification RPS |FullDataValidationRPS |Count/s |Total rows verified per second during full data verification. |
|Increment validation delay |IncrDataValidationDelay |s |During the incremental verification process, the time difference between the latest verified incremental position that has been fetched and the actual latest generated verification position. |

---
title: "Backfilling historical data to Prometheus"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Backfill_historical_data_to_Prometheus"
---

The Exporter provides the historical data backfill feature. If data loss occurs when monitoring data is being exported to Prometheus, you can manually backfill data. This topic describes how to backfill historical data.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Both historical data backfill and exporting monitoring data to self\-managed Prometheus are currently in the public beta stage. To use these features, enable pay\-as\-you\-go first and then contact your account manager.</div>


<span id="36ZH9IAl"></span>
## Background

The backfill task queries and exports historical monitoring data based on the product or metric range specified in the configuration and the current instance list. The metric point interval is defined by `DataFreshIntervalSeconds` (default value: 60 seconds), and the time range `[StartTime, EndTime)` is left\-closed and right\-open. In addition, if you enable the independent metadata metric `MetaLabelWithNewMetric`, which is disabled by default, an additional metadata time series for the current time will be exported.

<span id="omMRK6yu"></span>
## Prerequisites

The Exporter has been installed. You can install the Exporter on Kubernetes, Docker, or a virtual machine.

<span id="omMRK6yu"></span>
## Limits


* If the configured backfill time range is not aligned with the metric query interval `QueryPeriodSeconds`, which is set to the built\-in metric interval of the system by default, the query interval will be offset. Therefore, the system will automatically align the start and end time points to integer multiples of the query interval. For example, when the metric query interval is set to 30 seconds, the aligned start and end time points will be xx:xx:30 or xx:xx:00.

* To ensure that the data interval of each time series in the query results is consistent with that of the exported data, the time axis is divided into segments based on the current `DataFreshIntervalSeconds` (default value: 60 seconds) configured in the file. The data points within each segment are then aggregated through `StatisticsType`.

* The backfill task will ignore `QueryDelaySeconds`, which is set to the built\-in metric delay of the system by default. When you specify the backfill time range, you need to make sure that the end time is set appropriately to prevent delayed data reporting.


<span id="pTyHNZ9x"></span>
## Procedure

<span id="Y2b2K6MF"></span>
### Step 1: Allow RemoteWrite and enable out\-of\-order writing

Prometheus restricts data writing rules and does not allow writing data earlier than the last data point collected by Prometheus. Therefore, data point filling and data backfill must be performed through out\-of\-order writing.


1. Open the out\-of\-order writing window.

   ```YAML
   storage:
     tsdb:
       out_of_order_time_window: 10m # The time window. It must include the earliest backfill data time. For example, if you want to backfill monitoring data in the last 3 hours, make sure that the parameter value is at least 3 hours. We recommend that you set the value greater than 3 hours because the execution takes some time.
   ```
   

2. Enable the RemoteWrite capability of Prometheus.

   ```YAML
    # Add the --web.enable-remote-write-receiver parameter to Prometheus startup parameters.
   ./prometheus --web.enable-remote-write-receiver
   ```
   


<span id="b6pFpEhd"></span>
### Step 2: Configure data backfill

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">If you specify parameters related to historical data backfill for both the configuration file and startup parameters, the command line parameters take precedence.</div>


* <div data-tips="true" data-tips-type="default">In the command\-line quick start mode, the <code>-n</code> startup parameter allows the process to stay running without exiting after startup. You cannot specify this configuration by using the configuration file.</div>




<Tabs>
<Tab zoneid="XsAvuSZ7x1" title="Method 1: Update the configuration file">
<TabTitle>Method 1: Update the configuration file</TabTitle>

1. Add core configurations related to historical data backfill in the configuration file, which is `"/conf/config.yaml"` by default. Example:


```YAML
 # The core configurations of historical backfill.
BackfillConfig:
 Enable: true  # The switch for the historical backfill feature.
 StartTime: "2026-01-01T00:00:00+08:00"   # The start time, which can be in the RFC3339 format or in Unix seconds.
 EndTime: "2026-01-01T01:00:00+08:00"     # The end time, which can be in the RFC3339 format or in Unix seconds.

 # (Required) The remote push target.
RemoteWrites:
 - Name: "local-prom"   # The unique identifier, which is used as a tag in self-monitoring metrics to distinguish multiple remote-write targets.
 Username: "xxx"
 Password: "yyy"
 EndPoint: http://prometheus-ip:prometheus-port/api/v1/write  # The remote write address. You need to enter the address of your self-managed Prometheus or VMP workspace.
 Scope:
 - cloud-monitor  # Required. The business metric.
 - self-metric    # Optional. The self-monitoring metric.
```



2. Run the startup command `./exporter --config='your_config.yaml'` of the Exporter to run the configuration and start historical data backfill.


</Tab>
<Tab zoneid="vnXG56sHpM" title="Method 2: Perform a quick start by using the command line">
<TabTitle>Method 2: Perform a quick start by using the command line</TabTitle>

Add startup parameters related to historical data backfill in the Exporter startup command to quickly start historical data backfill. Example command:

```Bash
./exporter --config='your_config.yaml' --backfill --backfill-start "2026-01-05T00:00:00+08:00" --backfill-end "2026-01-05T12:00:00+08:00" -n
```



|Startup parameters |Descriptions |
|---|---|
|\-\-backfill |Enable backfill mode. |
|\-\-backfill\-start/end |Specify the time range, which can be in the RFC3339 format or Unix seconds. |
|\-\-no\-exit |Optional. If you set this parameter to true, the process will not actively exit after execution. This allows you to view the summary report in the console and check results by using the Web UI. Default value: false. |





</Tab>
</Tabs>


<span id="GFqTNP3Y"></span>
## Verifying results


* After you run the startup command of the Exporter, you can view detailed backfill progress by using the progress bar in the log.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_eb39bb4606cade6b589a7dc247faa1ff.png) </span>


* Check the logs for the port and root path that the Exporter listens on, and then log in to the console to view the backfill progress.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8e90f91925213259ffae5c2416b5450c.png) </span>

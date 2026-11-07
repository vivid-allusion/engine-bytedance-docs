---
title: "Exporter troubleshooting solutions"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Exporter_exception_troubleshooting_solution"
---

This topic describes the troubleshooting solutions provided by the export tool Exporter.

<span id="9718f4a4"></span>
## Troubleshooting solutions to common log errors

<span id="33c981cf"></span>
### WARN: estimate request latency bigger than 'DataFreshIntervalSeconds'

The Exporter cannot **retrieve metric data** within each interval. If the data cannot be retrieved, a **breakpoint** may occur under some configurations. The complete log is as follows:

```Bash
WARN: cost {} to finish collect all metric data for this interval with DataFreshIntervalSeconds={} total request count={}. you can adjust the configuration of exporter to eliminate this log.
```


If this error occurs, it indicates that the collection duration is too long, which may cause Prometheus to fail to retrieve data. For the solution, see [Metric breakpoints](https://docs.byteplus.com/en/docs/cloudmonitor/Exporter_exception_troubleshooting_solution#7c6c2f2b).

<span id="86ce20e7"></span>
### Error: Could not find operation ListExporterMetrics for version 2018\-01\-01

This Exporter feature is in the public beta stage and is temporarily available for free. To use this feature, enable pay\-as\-you\-go first and then contact your sales or after\-sales representative to add to the allowlist.

<span id="d38b1d44"></span>
### Error: Request was rejected because the request speed of this openAPI is beyond the current flow control limit

The configured QPS exceeds the upper limit. For the solution, see [Rate limiting for the LimitQPSGetMetricData API](https://docs.byteplus.com/en/docs/cloudmonitor/Exporter_exception_troubleshooting_solution#90d84d94).

<span id="97720bab"></span>
## Troubleshooting solutions to metric exceptions

<span id="06a20750"></span>
### Self\-monitoring metrics


1. We recommend that you import the following self\-monitoring grafana template of the Exporter, which only applies to Exporter v1.0.18 and later.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The following template is compatible only with Grafana v7.0.0 and later.   </div>
   

   
   |Template file |Version requirements |
   |---|---|
   |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fb322e55f09685be2984a776f010e30d.json" name="Exporter self-monitoring - Grafana template - 1.4.0.json">Exporter self-monitoring - Grafana template - 1.4.0.json</Attachment><br> |Applicable to Exporter v1.4.0 and later |
   |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_96a3a27ebf12ab351201fc9237b366a3.json" name="Exporter self-monitoring - Grafana template - 1.0.18.json">Exporter self-monitoring - Grafana template - 1.0.18.json</Attachment><br> |Applicable to Exporter v1.0.18 to 1.3.0 |
   

2. You can call the `/metrics` API to obtain metrics.

   
   |Metric Name |Metric tag |Metric type |Metric Definition |
   |---|---|---|---|
   |exporter_api_request_total |* action: the API for requesting the server. The API for querying metric data is GetMetricData.<br><br>* http_code: the status code returned by the API.<br><br>* error_code: the error code returned by the server.  The rate limiting error code is AccountFlowLimitExceeded.<br><br>* retry_count: The number of request retries. |counter |The total number of requests made by the exporter to the server API. |
   |exporter_api_request_latency_ms_bucket<br><br>exporter_api_request_latency_ms_count<br><br>exporter_api_request_latency_ms_sum ||histogram |The latency distribution of requests made by the exporter to the server API. Unit: milliseconds. |
   |exporter_strategy_last_pull_request_count |None |gauge |The number of requests made by the exporter to the GetMetricData API in the previous round. |
   |exporter_strategy_last_pull_latency_ms |None |gauge |The total period of time spent on all requests made by the exporter to the GetMetricData API in the previous round. |
   |exporter_strategy_discard_request_counter |None |counter |The total number of requests discarded due to backlog caused by an excessive number of instances/metrics. |
   |exporter_meta_object_count |* namespace<br><br>* sub_namespace |gauge |The number of product instances. |
   |exporter_meta_metric_count ||gauge |The number of product metrics. |
   


<span id="7c6c2f2b"></span>
### Metric breakpoints

You can troubleshoot metric breakpoints by using the self\-monitoring Grafana dashboard of the Exporter.


* **Throttling troubleshooting**: Observe metrics such as 429 AccountFlowLimitExceeded on the following dashboard. For solutions, see [LimitQPSGetMetricData API throttling](https://docs.byteplus.com/en/docs/cloudmonitor/Exporter_exception_troubleshooting_solution#90d84d94).

* **Collection timeout troubleshooting**: Observe the metric on the following dashboard. This metric indicates the total period of time taken for each collection, which is the data refresh interval and corresponds to the DataFreshIntervalSeconds configuration (default value: 60 seconds).

   If the metric continuously exceeds the value of DataFreshIntervalSeconds (default value: 60 seconds), all metric data cannot be collected for each collection. As a result, data loss is displayed in Prometheus. Recommended solutions:

   * If you can accept reduced metric accuracy, you can set DataFreshIntervalSeconds to a higher value, such as 120 seconds or 300 seconds. For details, see [LimitQPSGetMetricData API throttling](https://docs.byteplus.com/en/docs/cloudmonitor/Exporter_exception_troubleshooting_solution#90d84d94).

   * We recommend that you increase the value of the LimitQPSGetMetricData or DataConcurrency parameter based on your business requirements. If you do not know how to specify this parameter, you can delete these field configurations and use the default configuration because adaptive throttling is supported in v1.0.18\-rc1 and later.

   * Occasional jitters, such as network latency, may also cause collection timeouts, which cause the Prometheus collection cycle to be missed. We recommend that you increase the collection frequency of Prometheus. For example, set the value to 1/5 of DataFreshIntervalSeconds.

   ```YAML
   scrape_configs:
     - job_name: "exporter"
       scrape_interval: 5s
       static_configs:
         - targets: ["localhost:9898"]
   ```
   


<span id="3219a130"></span>
### Missing metrics or no data


1. Check whether the `<ip>:<port>/metrics` endpoint of the exporter can be accessed as expected.

2. Check whether the Exporter instance on the Status page in Prometheus is functioning as expected. You can also check it by querying the up metric in Prometheus.

3. Check whether this metric exists on the Cloud Monitor page.

4. Check the issue by using logs and debug logs.

5. If rate limiting is triggered, we recommend that you reduce the number of metrics.

6. Check whether the metric exists by using the `/meta/metric` endpoint.

7. Check whether the relevant instance exists by using the `/meta/object` endpoint. No metrics exist if no instances exist.

   1. Use the `/meta/metric` endpoint to obtain the Namespace and SubNamespace of the metric.

   2. View the response of the `/meta/object` endpoint to check whether the data that corresponds to `Namespace/SubNamespace` exists.

      For example, the following response indicates that monitoring instances exist only for metrics with the Namespace `VCM_RDS_MySQL` and the SubNamespace `deploy_monitor`.

      ```JSON
      {
          "VCM_RDS_MySQL/deploy_monitor": [
              {
                  "Dimensions": [
                      {
                          "Name": "ResourceID",
                          "Value": "mysql-68781f23efcc"
                      }
                  ],
                  "Instances": [
                      {
                          "Name": "ResourceID",
                          "Value": "mysql-68781f23efcc"
                      }
                  ]
              }
          ]
      }
      ```
      


<span id="f2a62238"></span>
### Large interval between data points

The default allowed metric latency is 120 seconds, which does not cause issues in most cases. If an issue is identified, you can increase the value of DelaySeconds in the configuration file based on your business requirements.

<span id="7faa3cbe"></span>
### Metric value mismatch


* You need to align the aggregation granularity when you verify whether the values exported by the Exporter are consistent with those on the Cloud Monitor page.

   1. You can specify the aggregation granularity of the Exporter by using the QueryPeriod parameter, which is set to 30 seconds by default.

   2. The aggregation granularity on the Cloud Monitor page is related to the selected time range.

      * If the time range is set to 1 hour, the aggregation granularity is set to 30 seconds by default.

      * If the time range is set to 1 day, the aggregation granularity is set to 60 seconds by default.

         Therefore, by default, the Exporter data is consistent with that on the Cloud Monitor page when the query time range is set to 1 hour, but may not be consistent with that when the query time range is set to 1 day.

* The step/interval parameters in Prometheus/Grafana queries may also affect the final query results. We recommend that you set the value to that of the DataFreshIntervalSeconds parameter of the exporter.

   * prometheus

   * grafana

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5fdae8d37b1543ada637bfba4a20066b~tplv-goo7wpa0wc-image.image) </span>


<span id="026effe7"></span>
### Rate limiting error

You can identify rate limiting errors by using the logs of the Exporter or by importing the preceding self\-monitoring metrics of the Grafana dashboard for the Exporter.

<span id="90d84d94"></span>
#### LimitQPSGetMetricData API rate limiting

The default quota for the Cloud Monitor API is 20 QPS. The rate limiting of Exporter requests to the API is controlled by the QPS parameter `LimitQPSGetMetricData` and the concurrency parameter `DataConcurrency`. In 1.0.18\-rc1 and later, Exporter adaptively and dynamically adjusts the rate based on the number of instances and metrics per request by default.


* If you deploy only one exporter instance within your account, we recommend that you directly set `LimitQPSGetMetricData` to the account limit (default account limit: 20).

* If you deploy multiple exporter instances within your account, we recommend that you delete the `LimitQPSGetMetricData` and `DataConcurrency` parameters and use the default adaptive rate limiting method.

* For 1.0.18\-rc0 and later, you can reduce the QPS of the Exporter requests to the cloud service and decrease quota usage by configuring the metric allowlist for collection to filter out metrics that you do not want to collect. For details, see [Cloud product metric queries](https://console.byteplus.com/cloud_monitor/docs).


Methods of resolving rate limiting issues through configuration:


* [Configure the metric allowlist for collection (1.0.18 and later)](https://docs.byteplus.com/en/docs/cloudmonitor/Exporter_exception_troubleshooting_solution#3e9e16a5)

* [Configure the SubNamespace allowlist for collection (1.0.18 and later)](https://docs.byteplus.com/en/docs/cloudmonitor/Exporter_exception_troubleshooting_solution#c05a06b4)

* [Increase the batch size for metric queries](https://docs.byteplus.com/en/docs/cloudmonitor/Exporter_exception_troubleshooting_solution#65a7111e)

* [Increase the data refresh interval](https://docs.byteplus.com/en/docs/cloudmonitor/Exporter_exception_troubleshooting_solution#b6d09f7d)


<span id="3e9e16a5"></span>
##### Configure the metric allowlist for collection (1.0.18 and later)

To collect only some metrics of the product, you can specify the OnlyIncludeMetrics field. Example:

```YAML
Region: cn-beijing
Credentials:
  AccessKey: '{ak}'
  SecretKey: '{sk}'
Products:
  - Namespace: VCM_ECS # The product for which you need to collect metrics.
    OnlyIncludeMetrics: # The metrics to be collected.
      Instance: # The SubNamespace of the metric.
        - CpuTotal # The specific metric name.
        - MemoryUsedUtilization # The specific metric name.
        - GpuUsedUtilization # The specific metric name.
      GPU: # The SubNamespace of the metric.
        - GpuUsedUtilization  # The specific metric name.
        - GpuMemoryUsedSpace  # The specific metric name.
```


<span id="c05a06b4"></span>
##### Configure the SubNamespace allowlist for collection (1.0.18 and later)

To collect only some SubNamespace metrics of the product, specify the OnlyIncludeSubNamespaces field. Example:

```YAML
Region: cn-beijing
Credentials:
  AccessKey: '{ak}'
  SecretKey: '{sk}'
Products:
  - Namespace: VCM_ECS # The product for which you need to collect metrics.
    OnlyIncludeSubNamespaces: # The metrics to be collected.
      - Instance # The SubNamespace of the metric.
```


<span id="65a7111e"></span>
##### Increase the batch size for metric queries

This method only applies to scenarios where a large number of product instances exist in a region. For example, more than 10 or even more than 1000 instances exist. For example, when you use the default value 10 for the BatchInstanceCount parameter, if 1000 instances exist, 1000/10=100 requests will be sent for each metric. If BatchInstanceCount is set to 50, only 1000/50=20 requests need to be sent, which reduces quota usage. However, this may increase request latencies in extreme cases.

```YAML
Region: cn-beijing
Credentials:
  AccessKey: '{ak}'
  SecretKey: '{sk}'
BatchInstanceCount: 50 # Default value: 10. Maximum value: 50.
Products:
  - Namespace: VCM_ECS # The product for which you need to collect metrics.
```


<span id="b6d09f7d"></span>
##### Increase the data refresh interval

If you accept reduced data accuracy, for example, changing from one data point per minute to one data point every two minutes, you can specify the `DataFreshIntervalSeconds` parameter.

```YAML
Region: cn-beijing
Credentials:
  AccessKey: '{ak}'
  SecretKey: '{sk}'
DataFreshIntervalSeconds: 120 # The data refresh interval. Default value: 60 seconds.
Products:
  - Namespace: VCM_ECS # The product for which you need to collect metrics.
```


When you specify the DataFreshIntervalSeconds parameter, you need to lower the value of LimitQPSGetMetricData or remove the LimitQPSGetMetricData parameter configuration to use adaptive configuration, which is supported in 1.0.18\-rc1 and later.

<span id="cb155779"></span>
#### ListMonitorObjectsV2 API rate limiting

This API is used to obtain the instance list of cloud products. The default quota for this API is 10. If multiple Exporter instances exist, we recommend that you allocate these 10 QPS proportionally based on the number of products for each Exporter, and set this by using the `LimitQPSMonitorObjectList` parameter. Occasional rate limiting on `LimitQPSMonitorObjectList` generally does not affect metric data pulling. This only affects the timeliness of metadata updates (such as delayed monitoring data for newly purchased instances).

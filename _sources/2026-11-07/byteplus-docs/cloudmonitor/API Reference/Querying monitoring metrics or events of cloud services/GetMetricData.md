---
title: "GetMetricData"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/GetMetricData"
---

Query the time series data aggregated for the specified metric within the selected time period.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* Before calling the API, attach the **CloudMonitorReadOnlyAccess** policy to the IAM user. Otherwise, the `User is not authorized to perform: cloudmonitor:GetMetricData on resource` error will occur. For detailed steps, see [Authorizing IAM users](https://docs.byteplus.com/en/docs/cloudmonitor/Granting_permissions_to_an_IAM_user).

* The `GetMetricData` API supports single\-metric queries and cannot query multiple metrics at a time.

* A root user and their IAM users can initiate a total of at most 20 `GetMetricData` API calls per second. If the QPS for this API exceeds 20, rate limiting will be triggered.

* A single request supports retrieval of monitoring data for up to 50 instances at a time, with a maximum of 1,440 data points per request.

   If you need to retrieve a large number of metrics and objects, rate limits may cause data retrieval failures. We recommend that you distribute requests evenly based on the time dimension.


<span id=".6K-35rGC6K-05piO"></span>
## Request description

Cloud Monitor is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/cloudmonitor/Service_address) topic to choose an access point that is optimal for your service region.


* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=GetMetricData&Version=2018\-01\-01


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=GetMetricData&serviceCode=Volc_Observe&version=2018-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |GetMetricData |The API name. The API name is `GetMetricData`. |
|Version |String |Yes |2018\-01\-01 |The API version. The current API version is `2018-01-01`. |
|StartTime |Integer |No |1648048800 |The start time of the time range. It is a Unix timestamp (in seconds), for example, 1632904500. |
|EndTime |Integer |No |1648049400 |The end time of the time range. It is a Unix timestamp (in seconds), for example, 1632904801.<br><br><br>* `EndTime` must be later than `StartTime`.<br><br>* `EndTime` ‌must not be set to a future timestamp.<br><br>* `EndTime` must be less than the sum of the number of days allowed for queries by the product and `StartTime`. |
|Instances |Array of [Instance](https://docs.byteplus.com/en/docs/39/16298#instance) |No |\- |Information of metrics to be queried.<br><br><br>* Multiple instances have a logical "OR" relationship.<br><br>* If the instance parameter is not passed in, monitoring data for all instances in the region will be returned. In this case, if the data volume is large, it may cause `max-select-point` to exceed the limit, affecting business operations. Exercise caution when you perform this operation.<br><br>   If an error occurs, see the causes and solutions related to `max-select-point` in the Error codes section. |
|MetricName |String |No |InTraffic |Name of the metric to be queried. For details, see the **MetricName** field for each cloud product on the [Cloud Monitor metric query](https://console.byteplus.com/cloud_monitor/metricDoc?tabKey=metric) page. |
|Namespace |String |No |VCM_EIP |The namespace of the metrics to be queried. For details, see the **Namespace** field for each product on the [Cloud Monitor metric query](https://console.byteplus.com/cloud_monitor/metricDoc?tabKey=metric) page. |
|Period |String |No |1 minute |The interval granularity for data to be queried. Seconds (s), minutes (m), hours (h), days (d), and weeks (w) are supported.<br><br><br>* For example, querying data within a 10\-minute period and dividing it by 1\-minute intervals will return 10 data points.<br><br>* When the selected time range is long, we recommend against using a small period as the time interval, as this may result in an excessively large dataset and may cause `max-select-bucket` to exceed the limit, impacting business operations. Exercise caution when you configure this field.<br><br>   If an error occurs, see the causes and solutions related to `max-select-bucket` in the Error codes section.<br><br>* For details on `StartTime` and `EndTime` offsets relative to `Period`, see [Period description](https://docs.byteplus.com/en/docs/39/16298#.cGVyaW9k6K-05piO). |
|GroupBy |Array of String |No |AlternativeDimensionName |The grouping dimensions of the metric to be queried. For dimension details, see the **Dimensions** of metrics for each product on the [Cloud Monitor metric query](https://console.byteplus.com/cloud_monitor/metricDoc?tabKey=metric) page.<br><br><br>* If no **Optional** mark is present in the **Dimension** column, it means there are no optional dimensions. By default, all dimensions are required and will be used as metric grouping dimensions.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">"Required" means that regardless of whether these Dimension parameters are specified, the returned dimensions will be grouped by these Dimensions.</div><br><br><br><div data-tips="true" data-tips-type="tip">For example, for the Cache for Redis metric <code>AggregatedTotalQps</code>, the Dimension column is <strong>ResourceID,Node</strong>.</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When only the Node parameter is passed in without ResourceID:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">Query condition: Node=xxx and ResourceID=\*</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">Grouping dimensions: Node,ResourceID</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When both Node and ResourceID parameters are passed in:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">Query condition: Node=xxx and ResourceID=yyy</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">Grouping dimensions: Node,ResourceID</div><br><br><br>* If the **Optional** mark is present in the **Dimension** column, it means there are optional Dimensions. In this case, you need to explicitly specify the GroupBy parameter when using the metric. You can see the [GroupBy description](https://docs.byteplus.com/en/docs/39/16298#.Z3JvdXBieeivtOaYjg==) for a configuration example of this field.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The SDK needs to be upgraded to the version below to allow dimension filtering with GroupBy.</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Python: version 1.0.37 or later</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Go: version 1.0.97 or later</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Java: version 0.1.75 or later</div><br> |
|SubNamespace |String |No |Instance |The dimension of the metric to be queried. The `SubNamespace` has different values available for different `namespaces`. For details, see the **SubNamespace** field for each product on the [Cloud Monitor metric query](https://console.byteplus.com/cloud_monitor/metricDoc?tabKey=metric) page. |
|StatisticsMethods |Array of String |No |avg |Specify the aggregation method for monitoring data. Currently supported aggregation methods are:<br><br><br>* `avg`: Average aggregation. This method calculates the arithmetic mean of all metric sample values within the same aggregation group.<br><br>* `sum`: Summation aggregation. This method computes the total sum of all metric values within the same aggregation group.<br><br>* `max`: Maximum aggregation. This method extracts the maximum value among all metric samples within the same aggregation group.<br><br>* `min`: Minimum aggregation. This method extracts the minimum value among all metric samples within the same aggregation group.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When multiple aggregation methods are configured, the <code>MetricDataResults</code> in the response will contain separate result sets for each method, with the <code>StatisticsMethods</code> field identifying the corresponding aggregation method.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">We recommend using the statistical methods provided in <a href="https://console.byteplus.com/cloud_monitor/docs">Cloud Monitor metric query</a> for data queries. Otherwise, there may be statistical errors.</div><br> |


<span id="instance"></span>
### Instance


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Dimensions |Array of [Dimension](https://docs.byteplus.com/en/docs/39/16298#dimension) |No |\- |Dimensions of the metric to be queried. For dimension details, see the **Dimensions** of metrics for each product on the [Cloud Monitor metric query](https://console.byteplus.com/cloud_monitor/metricDoc?tabKey=metric) page.<br><br><br>* Each dimension contains only one set of KV.<br><br>* When multiple dimensions exist, the logical relationship between them is "and." |


<span id="dimension"></span>
### Dimension


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Name |String |No |ResourceID |The key of the metric to retrieve. |
|Value |String |No |eip\-13fxxxx |Value of the corresponding key. |


<span id=".cGVyaW9k6K-05piO"></span>
### Period description

For example, querying data within a 10\-minute period and dividing it by 1\-minute intervals will return 10 data points.

When the selected time range is long, it is not recommended to use a small interval. Otherwise, the dataset may be excessively large. The backend enforces a large request rejection policy. Requests will fail when submitted parameters meet the following condition:

```bash
(EndTime - StartTime) / Period >= 5000
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In the above conditions, the units for <code>EndTime</code>, <code>StartTime</code>, and <code>Period</code> are all seconds (s).</div>


For the combination of `StartTime`, `EndTime`, and `Period` parameters, we recommend referring to the table below for their value ranges.


|Query time range (EndTime \- StartTime) |Time interval for data aggregation (Period) |
|---|---|
|(0~6] hours |30 seconds |
|(6, 24] hours |1m |
|(1~7] days |5m |
|(7~15] days |60 minutes |


When a `Period` value is specified, both `StartTime` and `EndTime` will be adjusted. The time points in the returned dataset will be aligned to the interval defined by `Period`. An aligned time point refers to a timestamp that is exactly divisible by the value of `Period`.

For example:


* If `Period` is set to 30s, the aligned time points within each minute are 0s and 30s.

* If `Period` is set to 20s, the aligned time points within each minute are 0s, 20s, and 40s.

* If `Period` is set to 10m, the aligned time points within each hour are 0m0s, 10m0s, 20m0s, 30m0s, 40m0s, and 50m0s.

* If `Period` is set to 24h, the aligned time point within the time range is 00:00:00 UTC+0.


For example, `StartTime` is 2023\-03\-02 00:00:00 and `EndTime` is 2023\-03\-05 00:00:00.

In UTC time, `StartTime` is 2023\-03\-01 16:00:00 and `EndTime` is 2023\-03\-04 16:00:00.

The returned dataset will include data at the aligned UTC time points: 2023\-03\-02 00:00:00, 2023\-03\-03 00:00:00, and 2023\-03\-04 00:00:00.

`StartTime` will always be shifted **backward** to the nearest aligned time point, and `EndTime` will always be shifted **forward** to the nearest aligned time point. As a result, the length of the returned dataset and the specific time points included may change, but the `StartTime` and `EndTime` parameter values themselves remain unchanged. Only the actual time interval selected for data query is adjusted.

<span id=".Z3JvdXBieeivtOaYjg=="></span>
### GroupBy description

GroupBy specifies the grouping dimensions used for metric queries. For dimension details, see the **Dimensions** of metrics for each product on the [Cloud Monitor metric query](https://console.byteplus.com/cloud_monitor/metricDoc?tabKey=metric) page.


* If no **Optional** mark is present in the **Dimension** column, it means there are no optional dimensions. By default, all dimensions are required and will be used as metric grouping dimensions.

   **Required** means that regardless of whether these Dimension parameters are specified, the returned dimensions will be grouped by these Dimensions.

   For example, for the Cache for Redis metric **AggregatedTotalQps**, the Dimension column is **ResourceID,Node**.

   * When only the Node parameter is passed in without ResourceID:

      * Query condition: Node=xxx and ResourceID=\*

      * Grouping dimensions: Node,ResourceID

   * When both Node and ResourceID parameters are passed in:

      * Query condition: Node=xxx and ResourceID=yyy

      * Grouping dimensions: Node,ResourceID

* If the **Optional** mark is present in the **Dimension** column, it means there are optional Dimensions. In this case, you need to explicitly specify the GroupBy parameter when using the metric.

   For example, for the Cloud Search metric **CacheHitRatio**, the Dimension column is **ResourceID,Node(Optional)** . The configuration example for a multi\-instance scenario is as follows:


```json
{
    "Instances": [
        {
            "Dimensions": [
                {
                    "Name": "ResourceID",
                    "Value": "eip-13fxxxx"
                },
                {
                    "Name": "Node",
                    "Value": "xxxx"
                }
            ]
        },
        {
            "Dimensions": [
                {
                    "Name": "ResourceID",
                    "Value": "eip-14dxxxx"
                },
                {
                    "Name": "Node",
                    "Value": "xxxx"
                }
            ]
        }
    ],
    "GroupBy": [
        "Node"
    ]
}
```


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=GetMetricData&Version=2018-01-01
Content-Type: application/json
{
    "EndTime": 1648049400,
    "GroupBy": [
        ""
    ],
    "Instances": [
        {
            "Dimensions": [
                {
                    "Name": "ResourceID",
                    "Value": "eip-13fxxxx"
                }
            ]
        }
    ],
    "MetricName": "InTraffic",
    "Namespace": "VCM_EIP",
    "Period": "1m",
    "StartTime": 1648048800,
    "StatisticsMethods": "avg",
    "SubNamespace": "Instance"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Data |Object of [Data](https://docs.byteplus.com/en/docs/39/16298#data) |\- |Returned data. |


<span id="data"></span>
### Data


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Unit |String |Bytes |The metric unit. |
|Period |String |1 minute |Time interval granularity for the query.<br><br><br>* **m**: Minute<br><br>* **s**: Second<br><br>* **h**: Hour<br><br>* **d**: Day<br><br>* **w**: Week |
|EndTime |Integer |1648049400 |The end timestamp of the selected query time range, in seconds. |
|Namespace |String |VCM_EIP |The namespace to which the metric belongs. |
|StartTime |Integer |1648048800 |The start timestamp of the selected query time range, in seconds. |
|MetricName |String |InTraffic |Name of the metric to be queried. |
|DescriptionCN |String |Inbound traffic |Metric name in Chinese. |
|DescriptionEN |String |EIP In Traffic |Metric name in English. |
|MetricDataResults |Array of [MetricData](https://docs.byteplus.com/en/docs/39/16298#metricdata) |\- |Queried metric data. |


<span id="metricdata"></span>
### MetricData


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Legend |String |eip_in_bytes |Alias of the metric name. |
|DataPoints |Array of [DataPoint](https://docs.byteplus.com/en/docs/39/16298#datapoint) |\- |Aggregated time series data for the specified metric within the specified time segment. |
|Dimensions |Array of [Dimension](https://docs.byteplus.com/en/docs/39/16298#dimension-response) |\- |Query conditions. |
|StatisticsMethods |String |avg |The aggregation method for query results in the `MetricDataResults`. Currently supported aggregation methods include `avg`, `sum`, `max`, and `min`.<br><br>When multiple aggregation methods are specified in the request, a separate set of results is generated for each method and identified by this field. |


<span id="datapoint"></span>
### DataPoint


|Parameters |type |Sample value |Description |
|---|---|---|---|
|Value |Float |864 |The value. |
|Timestamp |Integer |1648048800 |The timestamp (in seconds) of data collection. |


<span id="dimension-response"></span>
### Dimension


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Name |String |ResourceID |The key of the metric to retrieve. |
|Value |String |eip\-13fxxxx |Value of the corresponding key. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "Result": {
        "Data": {
            "Unit": "Bytes",
            "Period": "1m",
            "EndTime": 1648049400,
            "Namespace": "VCM_EIP",
            "StartTime": 1648048800,
            "MetricName": "InTraffic",
            "DescriptionCN": "Inbound traffic",
            "DescriptionEN": "EIP In Traffic",
            "MetricDataResults": [
                {
                    "Legend": "eip_in_bytes",
                    "DataPoints": [
                        {
                            "Value": 864,
                            "Timestamp": 1648048800
                        }
                    ],
                    "Dimensions": [
                        {
                            "Name": "ResourceID",
                            "Value": "eip-13fxxxx"
                        }
                    ],
                    "StatisticsMethods": "avg"
                }
            ]
        }
    },
    "ResponseMetadata": {
        "Env": "",
        "Action": "GetMetricData",
        "Region": "cn-beijing",
        "Service": "cloudmonitor",
        "Version": "2018-01-01",
        "RequestId": "20230604110420****100232280022D31"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

There are no error codes specific to this API. For more information, see [Error codes](https://docs.byteplus.com/en/docs/cloudmonitor/Common-error-codes).

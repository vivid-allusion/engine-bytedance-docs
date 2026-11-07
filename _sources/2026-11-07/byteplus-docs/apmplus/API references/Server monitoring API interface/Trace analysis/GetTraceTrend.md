---
title: "GetTraceTrend"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetTraceTrend"
---

Obtains the trend of reported Span events.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

Server\-side Monitoring has been deployed in multiple regions around the world to provide you with a more stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-server.cn\-beijing.byteplusapi.com.cn?Action=GetTraceTrend&Version=2026\-01\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For details, see [Common parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetTraceTrend |The API name. The API name is `GetTraceTrend`. |
|Version |String |Yes |2026\-01\-01 |The API version. The API version is `2026-01-01`. |
|StartTime |Long |Yes |1767196800 |The query start timestamp in seconds. |
|EndTime |Long |Yes |1767200400 |Query end timestamp in seconds. |
|GranularityUnit |String |Yes |s |The time granularity unit, such as "s", "m", and "h".<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">GranularityUnit and Granularity together align the start and end times and determine the time series data step, corresponding to the aggregation method on the page.</div><br> |
|Granularity |Long |Yes |30 |The time granularity value. |
|MinCallCostMillisecond |Long |Yes |100 |The minimum call duration. This is used to filter data. A value of 0 indicates no filtering.<br><br> |
|MaxCallCostMillisecond |Long |Yes |1,000 |The maximum call duration. This is used to filter data. A value of 0 indicates no filtering. |
|Filters |Array of [FilterCondition](https://docs.byteplus.com/en/docs/299/84299#filtercondition) |Yes |\- |The general\-purpose filter criteria, which correspond to the filter boxes on the page. If no filter is specified, an empty list can be passed in.<br><br>An item consists of key, op, and value, such as `span_type,in,server`. |
|ProjectName |String |No |default |The project name. |
|TagFilters |Array of [TagFilter](https://docs.byteplus.com/en/docs/299/84299#tagfilter) |Yes |\- |Tag filter condition. It is set to a value in the format of key\-value pairs, which corresponds to the tag filter feature on the page. If no filter is specified, an empty list can be passed in. |
|BusinessCarrier |String |No |agentkit_runtime |The business carrier. Valid value: agentkit_runtime.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If this parameter is set to <code>agentkit_runtime</code>, the values of the ProjectName and TagFilters parameters do not take effect.</div><br> |


<span id="filtercondition"></span>
### FilterCondition


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Op |String |No |in |The operator in the filter criteria. Valid values: in and not_in. |
|Key |String |No |call_service_type |Key of the filter condition. |
|Values |Array of String |No |['http'] |Value of the filter condition. |


<span id="tagfilter"></span>
### TagFilter


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Key |String |No |testKey |The tag key. |
|Values |Array of String |No |['testValue'] |The tag value. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-server.cn-beijing.byteplusapi.com.cn?Action=GetTraceTrend&Version=2026-01-01
{
    "StartTime": 1767196800,
    "EndTime": 1767200400,
    "GranularityUnit": "s",
    "Granularity": 30,
    "MinCallCostMillisecond": 100,
    "MaxCallCostMillisecond": 1000,
    "Filters": [
        {
            "Op": "in",
            "Key": "call_service_type",
            "Values": [
                ""
            ]
        }
    ],
    "ProjectName": "default",
    "TagFilters": [
        {
            "Key": "testKey",
            "Values": [
                ""
            ]
        }
    ],
    "BusinessCarrier": "agentkit_runtime"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Panel |Object of [MetricPanel](https://docs.byteplus.com/en/docs/299/84299#metricpanel) |\- |The metric time series data. |


<span id="metricpanel"></span>
### MetricPanel


|**Parameters** |**type** |**Sample value** |**Description** |
|---|---|---|---|
|Accuracy |Integer |0 |The data accuracy. The default value is 0. |
|TrendList |Array of [MetricTrend](https://docs.byteplus.com/en/docs/299/84299#metrictrend) |\- |The data time series. |


<span id="metrictrend"></span>
### MetricTrend


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Avg |Double |100 |Average value. |
|Tags |Array of [TagKV](https://docs.byteplus.com/en/docs/299/84299#tagkv) |\- |The tags related to the trend. The value is expressed as a triplet, such as `tag key,tag display name,tag value`. |
|Unit |String |% |Unit.<br><br><br>* %: The API will return data in the range from 0 to 1. When the value is visualized in the console, if % is used as the unit, the data returned by the API needs to be multiplied by 100 to ensure the value matches the unit.<br><br>* byte: The API will return the number of bytes. When the value is visualized in the console, unit conversion can be performed based on actual needs. For example, convert the unit to KiB or MiB. |
|Points |Array of [SeriesPoint](https://docs.byteplus.com/en/docs/299/84299#seriespoint) |\- |The trend points. The value is expressed as a triplet, such as `start timestamp,metric value,end timestamp`. |
|MetricName |String |report volume |The metric name. |
|MetricLabel |String |testLabel |The metric display label. |


<span id="tagkv"></span>
### TagKV


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Key |String |testKey |Tag key. |
|Label |String |testLabel |The tag display name. |
|Value |String |testValue |Tag value. |


<span id="seriespoint"></span>
### SeriesPoint


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Value |Double |100 |The metric value. |
|Timestamp |Long |1640995200 |The start timestamp. |
|EndTimestamp |Long |1640995260 |The end timestamp. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "Result": {
        "Panel": {
            "Accuracy": 0,
            "TrendList": [
                {
                    "Avg": 100,
                    "Tags": [
                        {
                            "Key": "testKey",
                            "Label": "testLabel",
                            "Value": "testValue"
                        }
                    ],
                    "Unit": "%",
                    "Points": [
                        {
                            "Value": 100,
                            "Timestamp": 1640995200,
                            "EndTimestamp": 1640995260
                        }
                    ],
                    "MetricName": "report volume",
                    "MetricLabel": "testLabel"
                }
            ]
        }
    },
    "ResponseMetadata": {
        "Action": "GetTraceTrend",
        "Region": "cn-north-1",
        "Service": "apmplus_server",
        "Version": "2026-01-01",
        "RequestId": "20230604110420****100232280022D31"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

If the API call returns an exception, you can troubleshoot by referring to the API error codes and the [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) below.


|**HTTP status codes** |**Error codes** |**Error messages** |**Description** |
|---|---|---|---|
|500 |ErrInternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |

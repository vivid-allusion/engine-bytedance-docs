---
title: "GetAidQuotaUsedTrend"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAidQuotaUsedTrend"
---

Get the resource usage trend of a specified service for a specified application.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetAidQuotaUsedTrend&Version=2022\-10\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAidQuotaUsedTrend |The API name. The current API name is `GetAidQuotaUsedTrend`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|start_time |Long |Yes |1665417600 |Query start time. |
|end_time |Long |Yes |1666083280 |Query end time. |
|granularity |String |Yes |week |Time aggregation granularity.<br><br><br>* week<br><br>* day<br><br>* month |
|aid |Long |Yes |12345 |Application ID. |
|service_key |String |Yes |webpro_monitor |Specify a service. Available values can be obtained via the `GetServiceList` method. |
|os |String |No |\- |Required only when service_key is app_monitor. Pass Android or iOS. If not passed, it means all. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetAidQuotaUsedTrend&Version=2022-10-12
{
    "start_time": 1665417600,
    "end_time": 1666083280,
    "granularity": "week,day,month",
    "aid": 12345,
    "service_key": "webpro_monitor"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [EventTrendData](https://docs.byteplus.com/en/docs/299/67858#eventtrenddata) |\- |Resource usage trend. |
|error_msg |String |"" |Error message. It is empty if the request succeeds. |
|error_no |Integer |0 |Error code. 0 indicates success. |


<span id="eventtrenddata"></span>
### EventTrendData


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|total |Object of [TrendLine](https://docs.byteplus.com/en/docs/299/67858#trendline) |\- |Total usage trend. |
|modules |Array of [TrendLine](https://docs.byteplus.com/en/docs/299/67858#trendline) |\- |Usage trend of each module under a specific service. |


<span id="trendline"></span>
### TrendLine


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|name |String |test123 |The name of the line. When grouped, the name needs to be set to the value of the grouping dimension. For example, it is used as the legend label for the curve. |
|points |Array of [TrendPoint](https://docs.byteplus.com/en/docs/299/67858#trendpoint) |\- |The data points on the curve. |


<span id="trendpoint"></span>
### TrendPoint


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|alert |Object of [AlertPoint](https://docs.byteplus.com/en/docs/299/67858#alertpoint) |\- |The alert message. |
|value |Double |123 |The metric value. |
|timestamp |Long |1665417600 |Unix timestamp. |
|readable_timestamp |String |2022\-10\-11 |Calendar time. |


<span id="alertpoint"></span>
### AlertPoint


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|msg |String |\- |The alert message. |
|alert |Boolean |true |Whether an alert is required. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "data": {
        "modules": [
            {
                "name": "test123",
                "points": [
                    {
                        "timestamp": 1665417600,
                        "readable_timestamp": "2022-10-11",
                        "alert": {
                            "msg": "",
                            "alert": true
                        },
                        "value": 123
                    }
                ]
            }
        ],
        "total": {
            "name": "test123",
            "points": [
                {
                    "readable_timestamp": "2022-10-11",
                    "alert": {
                        "msg": "",
                        "alert": true
                    },
                    "value": 123,
                    "timestamp": 1665417600
                }
            ]
        }
    },
    "error_no": 0,
    "error_msg": ""
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.

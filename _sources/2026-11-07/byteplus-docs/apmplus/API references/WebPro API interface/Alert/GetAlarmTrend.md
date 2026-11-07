---
title: "GetAlarmTrend"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAlarmTrend"
---

Get the alert trend.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetAlarmTrend&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAlarmTrend |The API name. The current API name is `GetAlarmTrend`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|common |Object of [Common](https://docs.byteplus.com/en/docs/299/67936#common) |No |\- |Public parameters. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/67936#timefilter) |No |\- |Time range. |
|id |Long |No |302 |Alert task ID. |

### Common

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |No |12345 |Application ID. |
|os |String |No |webpro |Service type. |

### TimeFilter

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|start_time |Integer |No |1665849600 |Start time. |
|granularity |Integer |No |60 |Aggregation time granularity. |
|end_time |Integer |No |1666011403 |End time. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetAlarmTrend&Version=2022-10-12
{
    "common":{
        "aid":12345,
        "os":"webpro"
    },
    "id":302,
    "time_filter":{
        "start_time":1665849600,
        "end_time":1666011403,
        "granularity":3600
    }
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [Data](https://docs.byteplus.com/en/docs/299/67936#data) |\- |Response data. |

### Data

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|alarm_trend |Object of [AlarmTrend](https://docs.byteplus.com/en/docs/299/67936#alarmtrend) |\- |Alert trend. |

### AlarmTrend

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|fields |Array of [Fields](https://docs.byteplus.com/en/docs/299/67936#fields) |\- |Metric fields. |
|source |Array of String |[ "2022\-10\-11 08:00:00", "0" ] |The value corresponding to the field. |

### Fields

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |String |data |Alert time, which is what source[i][0] represents. |
|dataType |String |string |Data type. |
|name |String |date |Field name. |

## Sample response

```JSON
{
    "err_detail":"",
    "data":{
        "alarm_trend":{
            "fields":[
                {
                    "id":"date",
                    "dataType":"string",
                    "name":"date"
                },
                {
                    "id":"alarm_count",
                    "dataType":"number",
                    "name":"alert count"
                }
            ],
            "source":[
                [
                    "2022-10-11 08:00:00",
                    "0"
                ],
                [
                    "2022-10-17 08:00:00",
                    "156"
                ]
            ]
        }
    },
    "error_msg":"",
    "error_no":0
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.

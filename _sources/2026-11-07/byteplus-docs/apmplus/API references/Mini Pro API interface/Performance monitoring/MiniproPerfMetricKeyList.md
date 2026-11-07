---
title: "MiniproPerfMetricKeyList"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/MiniproPerfMetricKeyList"
---

View the performance monitor metric list.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=MiniproPerfMetricKeyList&Version=2024\-03\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |MiniproPerfMetricKeyList |The API name. The current API name is `MiniproPerfMetricKeyList`. |
|Version |String |Yes |2024\-03\-12 |The API version. The current API version is `2024-03-12`. |
|common |Object of [Common](https://docs.byteplus.com/en/docs/299/120624#common) |No |\- |Common parameters. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/120624#timefilter) |No |\- |Time filtering. |
|evtype |String |No |app_launch_perf |Event type.<br><br><br>* app_launch_perf : Launch performance<br><br>* page_perf: Page performance |

### Common

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |Yes |392926 |The app ID. |

### TimeFilter

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|start_time |Integer |Yes |1762088838 |Start time. |
|granularity |Integer |No |10800 |Aggregation granularity. |
|end_time |Integer |Yes |1762348038 |End time. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=MiniproPerfMetricKeyList&Version=2024-03-12
{
    "common": {
        "aid": 392926,
    },
    "time_filter": {
        "start_time": 1762088838,
        "end_time": 1762348038,
        "granularity": 10800
    },
    "evtype": "app_launch_perf"
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [Data](https://docs.byteplus.com/en/docs/299/120624#data) |\- |Returned data. |
|error_no |Integer |0 |Error code. |
|error_msg |String |"" |Error message. |

### Data

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|values |Array of [Values](https://docs.byteplus.com/en/docs/299/120624#values) |\- |Returned values. |

### Values

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |launch_perf_total_time_consume |Metric key. |
|calculate_types |Array of String |[<br><br>                    "AVG",<br><br>                    "PCT50",<br><br>                    "PCT75",<br><br>                    "PCT90",<br><br>                    "PCT95"<br><br>                ] |Supported aggregation calculation types. |
|description |String |First screen cold start total time |Description. |
|unit |String |ms |Unit. |

## Sample response

```JSON
{
    "err_detail": "",
    "data": {
        "values": [
            {
                "key": "launch_perf_total_time_consume",
                "calculate_types": [
                    "AVG",
                    "PCT50",
                    "PCT75",
                    "PCT90",
                    "PCT95"
                ],
                "description": "First screen total load time",
                "unit": "ms"
            },
            {
                "key": "slow_launch",
                "calculate_types": [
                    "COUNT"
                ],
                "description": "Slow start times",
                "unit": ""
            }
        ]
    },
    "error_msg": "",
    "error_no": 0
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.

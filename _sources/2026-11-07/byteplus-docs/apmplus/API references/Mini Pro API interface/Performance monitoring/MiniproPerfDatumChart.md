---
title: "MiniproPerfDatumChart"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/MiniproPerfDatumChart"
---

View the details of the performance monitor metric data.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=MiniproPerfDatumChart&Version=2024\-03\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |MiniproPerfDatumChart |The API name. The current API name is `MiniproPerfDatumChart`. |
|Version |String |Yes |2024\-03\-12 |The API version. The current API version is `2024-03-12`. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/120623#timefilter) |No |\- |Time filter. |
|common |Object of [Common](https://docs.byteplus.com/en/docs/299/120623#common) |No |\- |Common parameters. |
|filter_conditions |Object of [FilterConditions](https://docs.byteplus.com/en/docs/299/120623#filterconditions) |No |\- |Filter condition. |
|metric |String |No |launch_perf_total_time_consume |Performance monitor metric list. It can be obtained via the `MiniproPerfMetricKeyList` API. |

### TimeFilter

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|start_time |Integer |Yes |1762088942 |Start time. |
|granularity |Integer |No |10800 |Aggregation granularity. |
|end_time |Integer |Yes |1762348142 |End time. |

### Common

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |Yes |392926 |The app ID. |

### FilterConditions

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|type |String |Yes |and |The type of the filter condition.<br><br><br>* and: The conditions in children are in an "AND" relationship.<br><br>* rule: (default) The current condition is an atomic condition. |
|field |String |No |pid |Condition field. |
|op |String |No |in |Condition operators. Available values include: eq, neq, lt, lte, gt, gte, in, not_in, regex, not_regex. |
|values |Array of String |No |["test"] |Values of the filter condition. The set of available values can be obtained via the `MiniProGetFieldValues` API. |
|children |Array of |No |\- |Sub\-parameters of the filter condition. They are required only when the type value is `and`. <br><br>The children parameter can contain nested conditions but cannot coexist with op, field, or values. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=MiniproPerfDatumChart&Version=2024-03-12
{
    "common": {
        "aid": 392926,
    },
    "time_filter": {
        "start_time": 1762088942,
        "end_time": 1762348142,
        "granularity": 10800
    },
    "metric": "launch_perf_total_time_consume"
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [Data](https://docs.byteplus.com/en/docs/299/120623#data) |\- |Returned data. |
|error_msg |String |"" |Error message. |
|error_no |Integer |0 |Error code. |

### Data

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [Data](https://docs.byteplus.com/en/docs/299/120623#data) |\- |Returned data. |
|extra |JSON Map |\- |Extra information. |

### Extra

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |launch_perf_total_time_consume |Field key. |
|value |String |3416 |The field value. |

## Sample response

```JSON
{
    "err_detail": "",
    "data": {
        "data": {
            "fields": [
                {
                    "id": "duration",
                    "dataType": "number",
                    "name": ""
                },
                {
                    "id": "count",
                    "dataType": "number",
                    "name": "Total time consumption for cold start of the first screen"
                }
            ],
            "source": [
                [
                    "2000",
                    "419"
                ],
                [
                    "3000",
                    "692"
                ],
                [
                    "4000",
                    "311"
                ]
            ]
        },
        "extra": {
            "launch_perf_total_time_consume": "3416"
        }
    },
    "error_msg": "",
    "error_no": 0
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.

---
title: "MiniProGetFieldValues"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/MiniProGetFieldValues"
---

Get available values of specific filter criteria.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=MiniProGetFieldValues&Version=2024\-03\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |MiniProGetFieldValues |The API name. The current API name is `MiniProGetFieldValues`. |
|Version |String |Yes |2024\-03\-12 |The API version. The current API version is `2024-03-12`. |
|common |Object of [Common](https://docs.byteplus.com/en/docs/299/67998#common) |Yes |\- |Common parameters. |
|filter_conditions |Object of [FilterConditions](https://docs.byteplus.com/en/docs/299/67998#filterconditions) |No |\- |Filter conditions. They are nested. |
|field |String |No |pid |Filter dimension. Available values can be obtained via the `GetFieldKeys` API. |

### Common

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |Yes |12345 |Application ID. |

### FilterConditions

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|type |String |Yes |and |The type of the filter condition.<br><br><br>* and: The conditions in children are in an "AND" relationship.<br><br>* rule (default): The current condition is an atomic condition. |
|field |String |No |pid |Condition field. Available values can be obtained via the `GetFieldKeys` API. |
|op |String |No |in |Condition operator. Available values: eq, neq, lt, lte, gt, gte, in, not_in, regex, and not_regex. |
|values |Array of String |No |["Data explore"] |Condition values. |
|children |Array of [FilterConditions](https://docs.byteplus.com/en/docs/299/67998#filterconditions) |No |\- |Sub\-parameter. Required when the **type** value is `and`. Nesting is allowed under children, but it cannot coexist with op, field, or values. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=MiniProGetFieldValues&Version=2024-03-12
{
    "field": "pid",
    "common": {
        "aid": 12345
    },
    "time_filter": {
        "start_time": 1664621845,
        "end_time": 1665140253,
        "granularity": 86400
    },
    "filter_conditions": {
        "type": "and",
        "children": [
            {
                "op": "in",
                "field": "pid",
                "values": [
                    "data explore"
                ]
            }
        ]
    }
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Array of [Data](https://docs.byteplus.com/en/docs/299/67998#data) |\- |Response data. Available values can be obtained via the `GetFieldValues` API. |
|error_msg |String |\- |Error message. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### Data

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|value |String |Dashboards |Dimension value. |
|count |Long |3 |Number of event reports. |

## Sample response

```JSON
{
    "err_detail": "",
    "data": [
        {
            "value": "dashboard",
            "count": 3
        }
    ],
    "error_msg": "",
    "error_no": 0
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error, see [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.

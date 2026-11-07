---
title: "MiniProGetFieldKeys"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/MiniProGetFieldKeys"
---

Get filter conditions.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable endpoint based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=MiniProGetFieldKeys&Version=2024\-03\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |MiniProGetFieldKeys |The API name. The current API name is `MiniProGetFieldKeys`. |
|Version |String |Yes |2024\-03\-12 |The API version. The current API version is `2024-03-12`. |
|common |Object of [Common](https://docs.byteplus.com/en/docs/299/67999#common) |Yes |\- |Common parameters. |
|ev_type |String |Yes |performance |Module type.<br><br><br>* performance: Performance monitor<br><br>* js_error: JS monitoring<br><br>* http: Request monitor<br><br>* url_list: Page list<br><br>* custom: Custom monitor<br><br>* session: Data explore/session<br><br>* view: Data explore/view<br><br>* js_error: Data explore/JS error<br><br>* custom: Data explore/custom event<br><br>* log: Data explore/custom log |
|filter_conditions |Object of [FilterConditions](https://docs.byteplus.com/en/docs/299/67999#filterconditions) |No |\- |Time range. |

### Common

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |Yes |12345 |Application ID. |

### FilterConditions

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|type |String |Yes |and |The type of the filter condition.<br><br><br>* and: The conditions in children are in an "AND" relationship.<br><br>* rule (default): The current condition is an atomic condition. |
|field |String |No |pid |Condition field. |
|op |String |No |in |Condition operator. Available values: eq, neq, lt, lte, gt, gte, in, not_in, regex, and not_regex. |
|values |Array of String |No |["Data explore"] |Condition values. Available values can be obtained via the `GetFieldValues` API. |
|children |Array of [FilterConditions](https://docs.byteplus.com/en/docs/299/67999#filterconditions) |No |\- |Sub\-parameters. This parameter is required when the value of type is `and`. The children parameter can contain nested conditions but cannot coexist with op, field, or values. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=MiniProGetFieldKeys&Version=2024-03-12
{
    "ev_type": "performance",
    "common": {
        "aid": 12345
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
|data |Array of [Data](https://docs.byteplus.com/en/docs/299/67999#data) |\- |Response data. |
|error_msg |String |\- |Error message. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### Data

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|name |String |pid |Filter dimension. |
|description |String |pid |Description of the filter dimension. |
|renderForm |String |`RegexAndNotRegexEqAndNeqSymbol` |Supported filter methods for the filter dimension. |

## Sample response

```JSON
{
    "err_detail":"",
    "data":[
        {
            "name":"pid",
            "description":"pid",
            "renderForm":"RegexAndNotRegexEqAndNeqSymbol",
            "isDefault":false
        }
    ],
    "error_msg":"",
    "error_no":0
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.

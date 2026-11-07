---
title: "GetFieldKeys"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetFieldKeys"
---

Get filter criteria.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetFieldKeys&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetFieldKeys |The API name. The current API name is `GetFieldKeys`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|common |Object of [CommonParams](https://docs.byteplus.com/en/docs/299/67912#commonparams) |Yes |\- |Common parameter. |
|ev_type |String |Yes |performance |Module type.<br><br><br>* performance: Performance monitoring<br><br>* js_error: JS monitoring<br><br>* http: Request monitoring<br><br>* resource: Static resource monitoring<br><br>* url_list: Page list<br><br>* action: Action list<br><br>* custom: Custom monitoring<br><br>* blank_screen: Blank screen monitoring<br><br>* session: Data exploration/session<br><br>* view: Data exploration/view<br><br>* action: Data exploration/action<br><br>* js_error: Data exploration/js error<br><br>* http: Data exploration/request<br><br>* resource: Data exploration/resource<br><br>* resource_error: Data exploration/resource error<br><br>* custom: Data exploration/custom event<br><br>* log: Data exploration/custom log<br><br>* performance_longtask: Data exploration/long task<br><br>* blank_screen: Data exploration/blank screen |
|filter_conditions |Object of [FilterCondition](https://docs.byteplus.com/en/docs/299/67912#filtercondition) |No |\- |The filter condition. |

### CommonParams

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |Yes |12345 |Application ID. |
|site_type |String |Yes |web |Site type. |
|env |String |Yes |online |Environment. An empty string "" indicates all. |
|os |String |No |webpro |Service Type. Available values are **webpro**, **app**, and **minipro**. |
|user |String |No |test_user |Username. |

### FilterCondition

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|type |String |Yes |and |Filter condition type. Available values are **and** and **rule**. Only two levels are supported. The first level type must be "and", and the second level type must be "rule". |
|field |String |No |pid |Condition field key. Available values can be obtained via the `GetFieldKeys` API. |
|op |String |No |in |Condition operator. Available values: eq, neq, lt, lte, gt, gte, in, not_in, regex, not_regex. |
|groupKey |String |No |context |Map type field key. Available values can be obtained via the `GetFieldKeys` API. |
|values |Array of String |No |[Data explore] |Criterion values. Available values can be obtained via the `GetFieldValues` API. |
|children |Array of [FilterCondition](https://docs.byteplus.com/en/docs/299/67912#filtercondition) |No |\- |If there are conditions at the next level, put them here. This parameter is required when type is **and**. It cannot be specified together with field, op, groupKey, or values at this level. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetFieldKeys&Version=2022-10-12
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
|data |Array of [FieldKeysResp](https://docs.byteplus.com/en/docs/299/67912#fieldkeysresp) |\- |Response data. |
|error_msg |String |success |Error message. |
|error_no |Integer |500 |Error code. 0 indicates success. |

### FieldKeysResp

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|name |String |pid |Field name. |
|isDefault |Boolean |true |Whether it is the default. |
|renderForm |String |\- |Display form. |
|description |String |\- |Field description. |

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

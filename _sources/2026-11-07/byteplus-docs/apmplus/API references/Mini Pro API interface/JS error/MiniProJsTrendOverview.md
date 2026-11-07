---
title: "MiniProJsTrendOverview"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/MiniProJsTrendOverview"
---

View the JavaScript error trend overview.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=MiniProJsTrendOverview&Version=2024\-03\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |MiniProJsTrendOverview |The API name. The current API name is `MiniProJsTrendOverview`. |
|Version |String |Yes |2024\-03\-12 |The API version. The version of the current API is `2024-03-12`. |
|common |Object of [Common](https://docs.byteplus.com/en/docs/299/68005#common) |Yes |\- |Common parameters. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/68005#timefilter) |Yes |\- |Time interval. |
|filter_conditions |Object of [FilterConditions](https://docs.byteplus.com/en/docs/299/68005#filterconditions) |No |\- |The filter conditions. |

### Common

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |Yes |12345 |Application ID. |
|site_type |String |Yes |web |Site type. |
|env |String |Yes |online |Environment. An empty string ("") indicates all environments. |
|os |String |No |webpro |Service type. Optional values are **app**, **webpro**, and **minipro**. |
|user |String |No |test_user |Username. |

### TimeFilter

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|start_time |Integer |Yes |1665485413 |Start time. Unit: s. |
|granularity |Integer |No |3600 |Aggregation time granularity. Unit: s. |
|end_time |Integer |Yes |1665744613 |End time. Unit: s. |

### FilterConditions

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|type |String |Yes |and |The type of the filter condition.<br><br><br>* and: The conditions in children have an "AND" relationship.<br><br>* rule: The current condition is an atomic condition.<br><br>   Only two levels are supported. The "type" of the first level must be "and", and the "type" of the second level must be "rule". |
|children |Array of [ConditionChild](https://docs.byteplus.com/en/docs/299/68005#conditionchild) |No |\- |Sub\-parameter. This parameter is required when the value of type is `and`. |

### ConditionChild

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|type |String |Yes |rule |The type of the filter condition.<br><br><br>* and: The conditions in children are in an "AND" relationship.<br><br>* rule: The current condition is an atomic condition.<br><br>   Only two levels are supported. The "type" of the first level must be "and", and the "type" of the second level must be "rule". |
|field |String |No |pid |The key of the condition field. Available values can be obtained via the `GetFieldKeys` API. |
|op |String |No |in |Condition operators. Optional values are eq, neq, lt, lte, gt, gte, in, not_in, regex, not_regex. |
|groupKey |String |No |context |Key of a map\-type field. Available values can be obtained via the `GetFieldKeys` API. |
|values |Array of String |No |[data explore] |Condition values. The set of optional values can be obtained by the `GetFieldValues` method. |
|children |Array of [ConditionChild](https://docs.byteplus.com/en/docs/299/68005#conditionchild) |No |\- |The type of the filter condition.<br><br><br>* and: The conditions in children are in an "AND" relationship.<br><br>* rule: The current condition is an atomic condition.<br><br> <br><br>   Only two levels are supported. The "type" of the first level must be "and", and the "type" of the second level must be "rule". |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=MiniProJsTrendOverview&Version=2024-03-12
{
    "common": {
        "aid": 12345,
        "site_type": "web",
        "env": "online",
        "os": "webpro",
        "user": "test_user"
    },
    "time_filter": {
        "start_time": 1665485413,
        "end_time": 1665744613,
        "granularity": 3600
    },
    "filter_conditions": {
        "type": "and",
        "op": "in",
        "children": [
            {
                "type": "and",
                "children": [
                    {
                        "type": "and",
                        "values": "[data explore]",
                        "field": "pid",
                        "groupKey": "context",
                        "op": "in",
                        "children": [
                        ]
                    }
                ],
                "op": "in",
                "field": "pid",
                "values": "[data explore]",
                "groupKey": "context"
            }
        ],
        "field": "pid",
        "groupKey": "context",
        "values": "[data explore]"
    }
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [Data](https://docs.byteplus.com/en/docs/299/68005#data) |\- |Overview trend. |
|error_no |Integer |0 |Error code. 0 indicates success. |
|error_msg |String |\- |Error message. Empty indicates success. |

### Data

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|chart |Object of [Chart](https://docs.byteplus.com/en/docs/299/68005#chart) |\- |Custom event reporting trend. |
|info |Array of [Info](https://docs.byteplus.com/en/docs/299/68005#info) |\- |Custom event overview value. |
|extra |Object of [Extra](https://docs.byteplus.com/en/docs/299/68005#extra) |\- |Custom event extra information. |

### Chart

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|fields |Array of [Fields](https://docs.byteplus.com/en/docs/299/68005#fields) |\- |Line chart/pie chart dimension, len(fields)=len(source[i]). |
|source |Array of String |[["1668355200","js_error","0","0"]] |The set of specific points in the trend chart. len(source) is the number of points in the line chart or the number of blocks in the pie chart. |

### Info

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |String |count |Aggregate value key. |
|name |String |White\-screen count |Aggregate value name. |
|count |String |1 |Aggregated value. |
|unit |String |ms |Aggregation unit. |
|change |String |1.0 |Cycle\-on\-cycle. |

### Extra

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|release_info |Array of [ReleaseInfo](https://docs.byteplus.com/en/docs/299/68005#releaseinfo) |\- |Version release status. |

### Fields

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |String |date |Dimension key. |
|dataType |String |string |Dimension type. |
|name |String |Date |Dimension name. |
|aggregate |String |\- |Aggregation method. |

### ReleaseInfo

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|create_at |Integer |1668483578 |Version release date. |
|release |String |v2.2.123 |Version. |
|env |String |test |Version release environment. |
|commit |String |[] |Version\-related commit. |

## Sample response

```JSON
{
    "error_msg": "",
    "error_no": 0,
    "data": {
        "chart": {
            "source": [
                [
                    "1668355200",
                    "js_error",
                    "0",
                    "0"
                ]
            ],
            "fields": [
                {
                    "dataType": "string",
                    "name": "date",
                    "aggregate": "",
                    "id": "date"
                }
            ]
        },
        "extra": {
            "release_info": [
                {
                    "env": "test",
                    "create_at": 1668483578,
                    "release": "v2.2.123",
                    "commit": ""
                }
            ]
        },
        "info": [
            {
                "count": "1",
                "unit": "ms",
                "id": "count",
                "name": "White-screen count",
                "change": "1"
            }
        ]
    }
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.

---
title: "DataList"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/DataList"
---

Get the report details list for a specific type.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=DataList&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |DataList |The API name. The current API name is `DataList`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|common |Object of [CommonParams](https://docs.byteplus.com/en/docs/299/67948#commonparams) |Yes |\- |Common parameters. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/67948#timefilter) |Yes |\- |Time range. |
|filter_conditions |Object of [FilterCondition](https://docs.byteplus.com/en/docs/299/67948#filtercondition) |Yes |\- |The filter condition. |
|page_num |Integer |Yes |1 |Page number. |
|page_size |Integer |Yes |10 |Number of items per page. |
|ev_type |String |Yes |session |Reporting type. |

### CommonParams

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |Yes |12345 |Application ID. |
|site_type |String |Yes |web |Site type. |
|env |String |Yes |online |Environment. An empty string "" indicates all. |
|os |String |No |webpro |Service type. Available values are **webpro**, **app**, and **minipro**. |
|user |String |No |test_user |Username. |

### TimeFilter

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|start_time |Integer |Yes |1665485413 |Start time, in seconds. |
|end_time |Integer |Yes |1665744613 |End time, in seconds. |
|granularity |Integer |No |3600 |Aggregation time granularity, in seconds. |

### FilterCondition

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|type |String |Yes |and |Filter condition type. Available values are **and** and **rule**. Only two levels are supported. The type of the first level must be "and", and the type of the second level must be "rule". |
|field |String |No |pid |Condition field key. Available values can be obtained via the `GetFieldKeys` API. |
|op |String |No |in |Condition operators. Available values: eq, neq, lt, lte, gt, gte, in, not_in, regex, not_regex. |
|groupKey |String |No |context |Map type field key. Available values can be obtained via the `GetFieldKeys` API. |
|values |Array of String |No |[Data explore] |Criterion values. Available values can be obtained via the `GetFieldValues` API. |
|children |Array of [FilterCondition](https://docs.byteplus.com/en/docs/299/67948#filtercondition) |No |\- |If there are conditions at the next level, put them here. This parameter is required when type is **and**. This level cannot coexist with field, op, groupkey, and values. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=DataList&Version=2022-10-12
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
        "values": "[data explore]",
        "field": "pid",
        "op": "in",
        "children": [
            {
                "type": "and",
                "field": "pid",
                "children": [],
                "op": "in",
                "groupKey": "context",
                "values": "[data explore]"
            }
        ],
        "groupKey": "context"
    },
    "page_num": 1,
    "page_size": 10,
    "ev_type": "session"
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [DataListData](https://docs.byteplus.com/en/docs/299/67948#datalistdata) |\- |The report details list for the specified type. |
|error_msg |String |\- |Error message. Empty indicates success. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### DataListData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|count |Integer |10 |Total event reports. |
|table_list |Array of [DataListItem](https://docs.byteplus.com/en/docs/299/67948#datalistitem) |\- |List of report details for a specific page number, returned in reverse order of client time. |

### DataListItem

|**Parameters** |**type** |**Sample value** |**Description** |
|---|---|---|---|
|json |String |\- |Raw report JSON. |
|ev_type |String |session |Report type. |
|metric_map |JSON Map |\- |Report details. |

### MetricMap

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |browser_brand |Key of the report parameter. |
|value |Object of [MetricData](https://docs.byteplus.com/en/docs/299/67948#metricdata) | | |

### MetricData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|unit |String |ms |Unit of the dimension value. |
|label |String |browser_brand |Dimension name. |
|value |String |Chrome |The reported value of a dimension. |
|groupKey |String |\- |Key of the dimension group. |
|groupName |String |\- |Name of the dimension group. |

## Sample response

```JSON
{
    "data": {
        "table_list": [
            {
                "ev_type": "session",
                "json": "bored",
                "metric_map": "{\"browser_brand\":{\"value\":\"Chrome\",\"label\":\"browser_brand\",\"groupKey\":\"\",\"groupName\":\"\"},\"fcp\":{\"value\":\"1109.6\",\"label\":\"FCP\",\"unit\":\"ms\",\"groupKey\":\"\",\"groupName\":\"\"}"
            }
        ]
    },
    "error_no": 0,
    "error_msg": ""
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.

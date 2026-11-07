---
title: "JSOverviewPageList"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/JSOverviewPageList"
---

Get the list of pages where JavaScript errors occurred.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable endpoint based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=JSOverviewPageList&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |JSOverviewPageList |The API name. The API name is `JSOverviewPageList`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|common |Object of [CommonParams](https://docs.byteplus.com/en/docs/299/67955#commonparams) |Yes |\- |Common parameters. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/67955#timefilter) |Yes |\- |Time range. |
|filter_conditions |Object of [FilterCondition](https://docs.byteplus.com/en/docs/299/67955#filtercondition) |No |\- |The filter condition. |
|order_by |String |No |count_ascend |The sorting method.<br><br><br>* count_ascend<br><br>* count_descend<br><br>* user_ascend<br><br>* user_descend |
|pgno |Long |No |1 |Page number. |
|pgsz |Long |No |10 |Number of items per page. |

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
|op |String |No |in |Condition operators. Optional values are eq, neq, lt, lte, gt, gte, in, not_in, regex, and not_regex. |
|groupKey |String |No |context |Map type field key. The set of optional values can be obtained by the `GetFieldKeys` method. |
|values |Array of String |No |[data explore] |Condition values. The set of optional values can be obtained by the `GetFieldValues` method. |
|children |Array of [FilterCondition](https://docs.byteplus.com/en/docs/299/67955#filtercondition) |No |\- |If there are conditions at the next level, put them here. This parameter is required when type is **and**. This level cannot coexist with field, op, groupkey, and values. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=JSOverviewPageList&Version=2022-10-12
{
    "common": {
        "aid": 12345,
        "site_type": "web",
        "env": "online",
        "user": "test_user",
        "os": "webpro"
    },
    "time_filter": {
        "start_time": 1665485413,
        "end_time": 1665744613,
        "granularity": 3600
    },
    "filter_conditions": {
        "type": "and",
        "values": "[data explore]",
        "groupKey": "context",
        "field": "pid",
        "op": "in",
        "children": [
            {
                "type": "and",
                "groupKey": "context",
                "children": [],
                "op": "in",
                "field": "pid",
                "values": "[data explore]"
            }
        ]
    },
    "order_by": "count_ascend,count_descend,user_ascend,user_descend",
    "pgsz": 10,
    "pgno": 1
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|error_msg |String |\- |Error message. If the request was successful, this field is empty. |
|error_no |Integer |0 |Error code. 0 indicates success. |
|data |Object of [OverviewPageListResponseData](https://docs.byteplus.com/en/docs/299/67955#overviewpagelistresponsedata) |\- |An aggregated list of pages where JavaScript errors occurred. |

### OverviewPageListResponseData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|total |Long |10 |Total number of page clusters where JavaScript errors occurred. |
|result |Array of [PageListItem](https://docs.byteplus.com/en/docs/299/67955#pagelistitem) |\- |A list of pages with JavaScript errors for the specified page number. |

### PageListItem

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|pid |String |pid_test |Page ID (page_id). |
|user |Long |10 |Number of users affected by JavaScript errors. |
|count |Long |10 |Number of JavaScript errors in the error and user count data. |
|user_mini_chart |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67955#chartdata) |\- |The trend in the number of users affected by JavaScript errors. |
|count_mini_chart |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67955#chartdata) |\- |Trend in the number of JavaScript errors. |

### ChartData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|fields |Array of [Field](https://docs.byteplus.com/en/docs/299/67955#field) |\- |Dimensions of the line chart or pie chart. len(fields)=len(source[i]). |
|source |Array of String |[["1668355200","js_error","0","0"]] |The set of data points in the trend chart. len(source) is the number of points in the line chart or the number of slices in the pie chart. |

### Field

|**Parameters** |**type** |**Sample value** |**Description** |
|---|---|---|---|
|id |String |date |Dimension key. |
|name |String |Date |Dimension name. |
|dataType |String |string |Dimension type. |
|aggregate |String |\- |Aggregation method. |

## Sample response

```JSON
{
    "data": {
        "result": [
            {
                "pid": "pid_test",
                "user_mini_chart": {
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
                            "name": "date",
                            "id": "date",
                            "aggregate": "harpoon",
                            "dataType": "string"
                        }
                    ]
                },
                "count": 10,
                "count_mini_chart": {
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
                "user": 10
            }
        ],
        "total": 10
    },
    "error_msg": "",
    "error_no": 0
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.

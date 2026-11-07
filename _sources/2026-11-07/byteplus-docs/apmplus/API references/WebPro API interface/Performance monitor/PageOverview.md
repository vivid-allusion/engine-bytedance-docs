---
title: "PageOverview"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/PageOverview"
---

Get an overview of page performance metrics.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=PageOverview&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |PageOverview |The API name. The current API name is `PageOverview`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/67963#timefilter) |Yes |\- |Time range. |
|common |Object of [CommonParams](https://docs.byteplus.com/en/docs/299/67963#commonparams) |Yes |\- |Common parameter. |
|filter_conditions |Object of [FilterCondition](https://docs.byteplus.com/en/docs/299/67963#filtercondition) |No |\- |The filter condition. |
|type |String |Yes |avg |Performance metric aggregation method. |

### TimeFilter

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|start_time |Integer |Yes |1665485413 |Start time, in seconds. |
|end_time |Integer |Yes |1665744613 |End time, in seconds. |
|granularity |Integer |No |3600 |Aggregation time granularity, in seconds. |

### CommonParams

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |Yes |12345 |Application ID. |
|site_type |String |Yes |web |Site type. |
|env |String |Yes |online |Environment. An empty string "" indicates all. |
|os |String |No |webpro |Service type. Available values are **webpro**, **app**, and **minipro**. |
|user |String |No |test_user |Username. |

### FilterCondition

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|type |String |Yes |and |Filter condition type. Available values are **and** and **rule**. Only two levels are supported. The first level type must be "and", and the second level type must be "rule". |
|field |String |No |pid |Condition field key. Available values can be obtained via the `GetFieldKeys` API. |
|op |String |No |in |Condition operator. Available values: eq, neq, lt, lte, gt, gte, in, not_in, regex, not_regex. |
|groupKey |String |No |context |Map type field key. Available values can be obtained via the `GetFieldKeys` API. |
|values |Array of String |No |[Data explore] |Criterion values. Available values can be obtained via the `GetFieldValues` API. |
|children |Array of [FilterCondition](https://docs.byteplus.com/en/docs/299/67963#filtercondition) |No |\- |If there are conditions at the next level, put them here. This parameter is required when type is **and**. This level cannot coexist with field, op, groupkey, and values. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=PageOverview&Version=2022-10-12
{
    "time_filter": {
        "start_time": 1665485413,
        "end_time": 1665744613,
        "granularity": 3600
    },
    "common": {
        "aid": 12345,
        "site_type": "web",
        "env": "online",
        "user": "test_user",
        "os": "webpro"
    },
    "type": "avg",
    "filter_conditions": {
        "type": "and",
        "children": [
            {
                "type": "and",
                "groupKey": "context",
                "op": "in",
                "field": "pid",
                "children": [],
                "values": "[data explore]"
            }
        ],
        "op": "in",
        "values": "[data explore]",
        "field": "pid",
        "groupKey": "context"
    }
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Array of [PagePerfOverviewMetricItem](https://docs.byteplus.com/en/docs/299/67963#pageperfoverviewmetricitem) |\- |Performance metric overview. |
|error_msg |String |\- |Error message. Empty indicates success. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### PagePerfOverviewMetricItem

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|desc |String |\- |Performance metric description. |
|trend |Object of [PerfPageOverviewTrendDataWithExtra](https://docs.byteplus.com/en/docs/299/67963#perfpageoverviewtrenddatawithextra) |\- |Performance metric value trend. |
|metric |String |fp |Performance metric key. |
|status |Object of [PerfMetricStatus](https://docs.byteplus.com/en/docs/299/67963#perfmetricstatus) |\- |Performance metric status evaluation: As expected, above expected, or below expected. |
|bounce_rate |Object of [PerfPageOverviewTrendDataWithExtra](https://docs.byteplus.com/en/docs/299/67963#perfpageoverviewtrenddatawithextra) |\- |Trend of performance metric bounce rate. |
|distribution |Object of [PerfPageOverviewDistributionDataWithExtra](https://docs.byteplus.com/en/docs/299/67963#perfpageoverviewdistributiondatawithextra) |\- |Performance metric value distribution. |

### PerfPageOverviewTrendDataWithExtra

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67963#chartdata) |\- |Performance metric value trend. |
|extra |Object of [PerfPageOverviewTrendExtra](https://docs.byteplus.com/en/docs/299/67963#perfpageoverviewtrendextra) |\- |Additional information on performance metric values. |

### PerfMetricStatus

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|unit |String |ms |Performance metric unit. |
|level |Integer |0 |Level.<br><br><br>* 0: Severely below expected<br><br>* 1: Slightly below expected<br><br>* 2: As expected<br><br>* 3: Above expected |
|value |String |1234 |Performance metric value. |
|up_base_line |Double |2500 |Upper limit of the performance metric baseline. The value falling between the upper and lower limits is considered expected. |
|down_base_line |Double |1001 |The lower limit of the performance metric baseline. |

### PerfPageOverviewDistributionDataWithExtra

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67963#chartdata) |\- |Performance metric value distribution. |
|extra |Object of [PerfPageOverviewDistributionExtra](https://docs.byteplus.com/en/docs/299/67963#perfpageoverviewdistributionextra) |\- |Aggregated value of the performance metric. |

### ChartData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|fields |Array of [Field](https://docs.byteplus.com/en/docs/299/67963#field) |\- |Line chart/pie chart dimensions, len(fields)=len(source[i]). |
|source |Array of String |[["1668355200","js_error","0","0"]] |The set of specific points in the trend chart. len(source) is the number of points in the line chart or the number of blocks in the pie chart. |

### PerfPageOverviewTrendExtra

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|type |String |count,rate |Performance metric value unit. |
|benchmark |Double |2005 |The upper limit of the performance metric baseline.. |

### PerfPageOverviewDistributionExtra

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|up |Double |2500 |The upper limit of the performance metric baseline.. |
|down |Double |1001 |The lower limit of the performance metric baseline. |
|label |String |avg，pct50，pct75，pct90，pct95 |Performance metric aggregation method. |
|value |Double |1234 |Aggregated value of the performance metric. |
|granularity |String |50 |Distribution interval of performance metric values. |

### Field

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |String |date |Dimension key. |
|name |String |Date |Dimension name. |
|dataType |String |string |Dimension type. |
|aggregate |String |\- |Aggregation method. |

## Sample response

```JSON
{
    "error_msg": "",
    "data": [
        {
            "trend": {
                "data": {
                    "fields": [
                        {
                            "id": "date",
                            "aggregate": "",
                            "name": "date",
                            "dataType": "string"
                        }
                    ],
                    "source": [
                        [
                            "1668355200",
                            "js_error",
                            "0",
                            "0"
                        ]
                    ]
                },
                "extra": {
                    "benchmark": 2005,
                    "type": "count,rate"
                }
            },
            "status": {
                "value": "1234",
                "up_base_line": 2500,
                "level": 0,
                "unit": "ms",
                "down_base_line": 1001
            },
            "desc": "",
            "distribution": {
                "extra": {
                    "value": 1234,
                    "down": 1001,
                    "label": "avg，pct50，pct75，pct90，pct95",
                    "up": 2500,
                    "granularity": "50"
                },
                "data": {
                    "fields": [
                        {
                            "aggregate": "",
                            "dataType": "string",
                            "name": "date",
                            "id": "date"
                        }
                    ],
                    "source": [
                        [
                            "1668355200",
                            "js_error",
                            "0",
                            "0"
                        ]
                    ]
                }
            },
            "metric": "fp",
            "bounce_rate": {
                "data": {
                    "fields": [
                        {
                            "dataType": "string",
                            "name": "date",
                            "aggregate": "",
                            "id": "date"
                        }
                    ],
                    "source": [
                        [
                            "1668355200",
                            "js_error",
                            "0",
                            "0"
                        ]
                    ]
                },
                "extra": {
                    "benchmark": 2005,
                    "type": "count,rate"
                }
            }
        }
    ],
    "error_no": 0
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.

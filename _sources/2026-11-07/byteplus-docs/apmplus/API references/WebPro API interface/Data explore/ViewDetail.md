---
title: "ViewDetail"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/ViewDetail"
---

Get the performance and resource loading status under the specified view.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=ViewDetail&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ViewDetail |The API name. The current API name is `ViewDetail`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|common |Object of [CommonParams](https://docs.byteplus.com/en/docs/299/67949#commonparams) |Yes |\- |Common parameter. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/67949#timefilter) |Yes |\- |Time range. |
|event_id |String |Yes |http:[web_monitor]{webpro#session#649b8a7b\-5db4\-4989\-b9a5\-994e53da82ee#12345}:1663186696013#fc102ce5612345edb2bd00163e352627 |The unique identifier for reported data. It can be obtained from DataList.MetricMap. |

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

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=ViewDetail&Version=2022-10-12
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
    "event_id": "http:[web_monitor]{webpro#session#649b8a7b-5db4-4989-b9a5-994e53da82ee#12345}:1663186696013#fc102ce5612345edb2bd00163e352627"
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [ViewDetailResp](https://docs.byteplus.com/en/docs/299/67949#viewdetailresp) |\- |Performance and resource loading status under the specified view. |
|error_msg |String |\- |Error message. Empty indicates success. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### ViewDetailResp

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|navigation |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67949#chartdata) |\- |Performance duration Gantt chart. |
|rum_metric |JSON Map |\- |Performance metric value. |
|resources_waterfall |Object of [ChartDataWithExtra](https://docs.byteplus.com/en/docs/299/67949#chartdatawithextra) |\- |Resource loading status. |

### ChartData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|fields |Array of [Field](https://docs.byteplus.com/en/docs/299/67949#field) |\- |Line chart/pie chart dimensions, len(fields)=len(source[i]). |
|source |Array of String |[["1668355200","js_error","0","0"]] |The set of specific points in the trend chart. len(source) is the number of points in the line chart or the number of blocks in the pie chart. |

### RumMetric

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |\- |Performance metric key. |
|value |Object of [RumMetric](https://docs.byteplus.com/en/docs/299/67949#rummetric) | | |

### ChartDataWithExtra

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67949#chartdata) |\- |Returned data. |

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
    "error_no": 0,
    "error_msg": "",
    "data": {
        "navigation": {
            "fields": [
                {
                    "dataType": "string",
                    "id": "date",
                    "aggregate": "",
                    "name": "date"
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
        "resources_waterfall": {
            "data": {
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
                        "aggregate": "",
                        "dataType": "string"
                    }
                ]
            }
        }
    }
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.

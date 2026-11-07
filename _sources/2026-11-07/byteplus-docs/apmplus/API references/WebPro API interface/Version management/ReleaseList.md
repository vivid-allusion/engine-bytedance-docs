---
title: "ReleaseList"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/ReleaseList"
---

Get the list of versions.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable endpoint based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=ReleaseList&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ReleaseList |The API name. The API name is `ReleaseList`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|common |Object of [CommonParams](https://docs.byteplus.com/en/docs/299/67966#commonparams) |Yes |\- |Public parameters. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/67966#timefilter) |Yes |\- |Time range. |
|filter_name |String |No |v1. |Fuzzy search by version number. |
|env |String |No |online |Search for version numbers in the specified environment. If this parameter is not set, all environments are included. |
|page_no |Long |No |1 |Page number. |
|page_size |Long |No |10 |Number of items per page. |

### CommonParams

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |Yes |12345 |Application ID. |
|site_type |String |Yes |web |Site type. |
|env |String |Yes |online |Environment. An empty string "" indicates all. |
|os |String |No |webpro |Service type. Available values are **webpro**, **app**, and **minipro**. |
|user |String |No |test_user |Username. |

### TimeFilter

|**Parameters** |**type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|start_time |Integer |Yes |1665485413 |Start time, in seconds. |
|end_time |Integer |Yes |1665744613 |End time, in seconds. |
|granularity |Integer |No |3600 |Aggregation time granularity, in seconds. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=ReleaseList&Version=2022-10-12
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
    "page_size": 10,
    "env": "online",
    "page_no": 1,
    "filter_name": "v1."
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [ListResponseData](https://docs.byteplus.com/en/docs/299/67966#listresponsedata) |\- |A list of versions. |
|error_msg |String |\- |Error message. Empty indicates success. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### ListResponseData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Array of [ReleaseListInfo](https://docs.byteplus.com/en/docs/299/67966#releaselistinfo) |\- |Statistical version information for the specified page number. |
|total |Long |10 |Total number of versions. |

### ReleaseListInfo

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|env |String |online |Version release environment. |
|version |String |v1.2.3 |Version number. |
|pv_trend |Object of [ChartDataWithExtra](https://docs.byteplus.com/en/docs/299/67966#chartdatawithextra) |\- |The PV trend and PV overview value for this version. |
|deployed_at |Long |12345678 |The time of the first version report. |
|jserr_trend |Object of [ChartDataWithExtra](https://docs.byteplus.com/en/docs/299/67966#chartdatawithextra) |\- |The JavaScript error count trend and error count for this version. |
|new_jserr_trend |Object of [ChartDataWithExtra](https://docs.byteplus.com/en/docs/299/67966#chartdatawithextra) |\- |The trend and count of new JavaScript errors for this version. |

### ChartDataWithExtra

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67966#chartdata) |\- |Returned data. |

### ChartData

|**Parameters** |**type** |**Sample value** |**Description** |
|---|---|---|---|
|fields |Array of [Field](https://docs.byteplus.com/en/docs/299/67966#field) |\- |Dimensions of the line chart or pie chart. len(fields) = len(source[i]). |
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
    "error_no": 0,
    "data": {
        "data": [
            {
                "new_jserr_trend": {
                    "data": {
                        "fields": [
                            {
                                "aggregate": "",
                                "name": "date",
                                "id": "date",
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
                    }
                },
                "deployed_at": 12345678,
                "version": "v1.2.3",
                "jserr_trend": {
                    "data": {
                        "fields": [
                            {
                                "name": "date",
                                "dataType": "string",
                                "id": "date",
                                "aggregate": ""
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
                "pv_trend": {
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
                                "aggregate": "",
                                "id": "date",
                                "dataType": "string",
                                "name": "date"
                            }
                        ]
                    }
                },
                "env": "online"
            }
        ],
        "total": 10
    },
    "error_msg": ""
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.

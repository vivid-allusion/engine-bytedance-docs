---
title: "ReleaseDetail"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/ReleaseDetail"
---

Get the details of the specified version.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable endpoint based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=ReleaseDetail&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ReleaseDetail |The API name. The current API name is `ReleaseDetail`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|common |Object of [CommonParams](https://docs.byteplus.com/en/docs/299/67967#commonparams) |Yes |\- |General parameter. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/67967#timefilter) |Yes |\- |Time range. |
|release |String |Yes |v1.2.3 |Version number. |
|env |String |Yes |online |Release environment. |

### CommonParams

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |Yes |12345 |Application ID. |
|site_type |String |Yes |web |Site type. |
|env |String |Yes |online |Environment. If empty, includes all. |
|os |String |No |webpro |Service type. Optional values are **webpro**, **app**, **minipro**. |
|user |String |No |test_user |Username. |

### TimeFilter

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|start_time |Integer |Yes |1665485413 |Start time, in seconds. |
|end_time |Integer |Yes |1665744613 |End time, in seconds. |
|granularity |Integer |No |3600 |Aggregation time granularity, in seconds. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=ReleaseDetail&Version=2022-10-12
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
    "release": "v1.2.3",
    "env": "online"
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [ReleaseDetailResponseData](https://docs.byteplus.com/en/docs/299/67967#releasedetailresponsedata) |\- |Version details. |
|error_msg |String |\- |Error message. Empty indicates success. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### ReleaseDetailResponseData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|trend |Object of [ReleaseTrendInfo](https://docs.byteplus.com/en/docs/299/67967#releasetrendinfo) |\- |Change trend of PV, UV, JS error count, JS error aggregation issue count, new JS error count, and new JS aggregation issue count for the specified version. |
|jserr_info |Object of [ReleaseJSErrorInfo](https://docs.byteplus.com/en/docs/299/67967#releasejserrorinfo) |\- |JS error information for the specified version. |
|overview_info |Object of [ReleaseOverviewInfo](https://docs.byteplus.com/en/docs/299/67967#releaseoverviewinfo) |\- |Overview information of the specified version. |

### ReleaseTrendInfo

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|pv_uv |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67967#chartdata) |\- |Two lines that represent PV and UV. |
|err_count |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67967#chartdata) |\- |Error count. It returns two lines, representing the number of new error aggregation issues and the total number of error aggregation issues. |
|err_times |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67967#chartdata) |\- |Error count. It returns two lines, representing the number of new errors and the total number of errors. |

### ReleaseJSErrorInfo

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|new |Array of [NewJSErrorInfo](https://docs.byteplus.com/en/docs/299/67967#newjserrorinfo) |\- |List of new JS errors. |
|fixed |Array of [FixedJSErrorInfo](https://docs.byteplus.com/en/docs/299/67967#fixedjserrorinfo) |\- |List of fixed JS errors. |

### ReleaseOverviewInfo

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|uv |Long |10 |Unique visitor count. |
|env |String |online |Version release environment. |
|version |String |v1.2.3 |Version number. |
|created_at |Long |12345678 |Version creation time. |
|deployed_at |Long |12345678 |Deployment time. |
|jserr_count |Long |10 |JS aggregation issue count. |
|jserr_times |Long |10 |JS error count. |
|finalized_at |Long |12345678 |Version end time. |
|new_jserr_count |Long |10 |New JS aggregate issue count. |
|new_jserr_times |Long |10 |New JS error count. |

### ChartData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|fields |Array of [Field](https://docs.byteplus.com/en/docs/299/67967#field) |\- |Line chart/pie chart dimensions, len(fields)=len(source[i]). |
|source |Array of String |[["1668355200","js_error","0","0"]] |The set of specific points in the trend chart. len(source) is the number of points in the line chart or the number of blocks in the pie chart. |

### NewJSErrorInfo

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|name |String |TypeError |JS error type. |
|message |String |variable z not defined |JS error information. |
|filename |String |12345.js |Error file name. |
|issue_id |String |e2ed7046a625307277d8498b2cf0c11f |JS error aggregation ID. |

### FixedJSErrorInfo

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|name |String |TypeError |JS error type. |
|message |String |variable z not defined |JS error information. |
|filename |String |12345.js |Error file name. |
|issue_id |String |e2ed7046a625307277d8498b2cf0c11f |JS error aggregation ID. |
|commit_url |String |\- |Associated commit URL. |
|commit_message |String |\- |Commit information. |

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
        "overview_info": {
            "deployed_at": 12345678,
            "jserr_times": 10,
            "finalized_at": 12345678,
            "created_at": 12345678,
            "new_jserr_times": 10,
            "env": "online",
            "version": "v1.2.3",
            "jserr_count": 10,
            "new_jserr_count": 10,
            "uv": 10
        },
        "jserr_info": {
            "fixed_url": "",
            "new_url": "",
            "fixed": [
                {
                    "filename": "12345.js",
                    "commit_url": "",
                    "issue_id": "e2ed7046a625307277d8498b2cf0c11f",
                    "commit_message": "and",
                    "name": "TypeError",
                    "message": "variable z not defined"
                }
            ],
            "new": [
                {
                    "message": "variable z not defined",
                    "filename": "12345.js",
                    "name": "TypeError",
                    "issue_id": "e2ed7046a625307277d8498b2cf0c11f"
                }
            ]
        },
        "commit_info": [
            {
                "url": "situation",
                "time": 965,
                "author": "",
                "message": ""
            }
        ],
        "trend": {
            "err_count": {
                "fields": [
                    {
                        "id": "date",
                        "aggregate": "",
                        "dataType": "string",
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
            "err_times": {
                "fields": [
                    {
                        "name": "date",
                        "id": "date",
                        "dataType": "string",
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
            },
            "pv_uv": {
                "fields": [
                    {
                        "id": "date",
                        "aggregate": "",
                        "dataType": "string",
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
            }
        }
    }
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.

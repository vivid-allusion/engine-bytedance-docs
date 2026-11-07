---
title: "MiniProJsErrDetail"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/MiniProJsErrDetail"
---

Get JavaScript error details.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=MiniProJsErrDetail&Version=2024\-03\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |MiniProJsErrDetail |The API name. The current API name is `MiniProJsErrDetail`. |
|Version |String |Yes |2024\-03\-12 |The API version. The current API version is `2024-03-12`. |
|common |Object of [Common](https://docs.byteplus.com/en/docs/299/68003#common) |Yes |*  |Common parameters. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/68003#timefilter) |Yes |*  |Time range. |
|issue_id |String |Yes |2769ad7223a4eaefffbe9b2f59bb933b |JavaScript error aggregation ID. |

### Common

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |Yes |12345 |Application ID. |
|site_type |String |Yes |web |Site type. |
|env |String |Yes |online |Environment. An empty string ("") indicates all environments. |
|os |String |No |minipro |Service type. Available values are **webpro**, **app**, and **minipro**. |
|user |String |No |test_user |Username. |

### TimeFilter

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|start_time |Integer |Yes |1665485413 |Start time, in seconds. |
|granularity |Integer |No |3600 |Aggregation time granularity, in seconds. |
|end_time |Integer |Yes |1665744613 |End time, in seconds. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=MiniProJsErrDetail&Version=2024-03-12
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
    "issue_id": "2769ad7223a4eaefffbe9b2f59bb933b"
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [Data](https://docs.byteplus.com/en/docs/299/68003#data) |\- |JavaScript error details. |
|error_msg |String |\- |Error message. It is empty if the request succeeds. |
|error_no |Integer |0 |Error code. It is 0 if the request succeeds. |

### Data

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|name |String |\- |Error name and error message type. |
|message |String |Error: message test |Error message. |
|filename |String |12345.js |File name where the error occurred. |
|user |Long |10 |Error and user count information: Number of users affected by the JavaScript error. |
|count |Long |10 |Number of JavaScript errors. |
|issue_id |String |1234567223a4eaefffbe9b2f59bb933b |Issue\-related information. |
|issue |Object of [Issue](https://docs.byteplus.com/en/docs/299/68003#issue) |\- |Issue status operation |

### Issue

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |Long |\- |The issue ID in MySQL. It is different from issue_id. |
|managers |Array of [Managers](https://docs.byteplus.com/en/docs/299/68003#managers) |\- |Issue assignee. |
|status |String |processing |Issue status. |
|fixed_version |String |v1.1.2 |The fixed version. |

### Managers

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|name |String |test_user |Assignee name. |
|user_id |Long |12 |Assignee ID. |
|head_url |String |\- | |
|email |String |test_user@test.com |Assignee email. |

## Sample response

```JSON
{
    "data": {
        "extra": {
            "release_info": [
                {
                    "commit": "",
                    "create_at": 1668483578,
                    "env": "test",
                    "release": "v2.2.123"
                }
            ]
        },
        "release_distribution": {
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
                    "aggregate": "",
                    "dataType": "string",
                    "id": "date"
                }
            ]
        },
        "releases": [
        ],
        "message": "Error: message test",
        "trends": {
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
                    "aggregate": "",
                    "id": "date",
                    "dataType": "string"
                }
            ]
        },
        "issue": {
            "fixed_version": "v1.1.2",
            "tag": [
                {
                    "key": "",
                    "id": 172,
                    "values": [
                        {
                            "value": "",
                            "id": 346
                        }
                    ]
                }
            ],
            "managers": [
                {
                    "head_url": "",
                    "email": "test_user@test.com",
                    "name": "test_user",
                    "user_id": 12
                }
            ],
            "status": "processing",
            "id": 944
        },
        "max_crash_pid": "pid_2",
        "meego_issue_url": "powerful",
        "issue_id": "1234567223a4eaefffbe9b2f59bb933b",
        "filename": "12345.js",
        "git_issue_url": "I'm",
        "user": 10,
        "count": 10,
        "min_crash_time": 1668561659926,
        "name": "together",
        "pid_distribution": {
            "fields": [
                {
                    "id": "date",
                    "dataType": "string",
                    "name": "date",
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
        "max_crash_release": "v1.2.4",
        "min_crash_release": "v1.2.3",
        "max_crash_time": 1678561659926,
        "min_crash_pid": "pid_1"
    },
    "error_no": 0,
    "error_msg": ""
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.

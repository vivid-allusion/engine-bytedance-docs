---
title: "MiniProJsErrDetailStack"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/MiniProJsErrDetailStack"
---

Get JavaScript error stack trace information.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable endpoint based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=MiniProJsErrDetailStack&Version=2024\-03\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |MiniProJsErrDetailStack |The API name. The API name is `MiniProJsErrDetailStack`. |
|Version |String |Yes |2024\-03\-12 |The API version. The current API version is `2024-03-12`. |
|common |Object of [Common](https://docs.byteplus.com/en/docs/299/68002#common) |Yes |\- |Common parameters. |
|issue_id |String |Yes |1234567223a4eaefffbe9b2f59bb933b |JavaScript error aggregation ID. |
|release |String |No |v1.2.3 |Version where the JavaScript error occurred. |

### Common

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |Yes |12345 |Application ID. |
|site_type |String |Yes |web |Site type. |
|env |String |Yes |online |Environment. An empty string ("") indicates all environments. |
|os |String |No |minipro |Service type. Available values are **webpro**, **app**, and **minipro**. |
|user |String |No |test_user |Username. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=MiniProJsErrDetailStack&Version=2024-03-12
{
    "common": {
        "aid": 12345,
        "site_type": "web",
        "env": "online",
        "user": "test_user",
        "os": "webpro"
    },
    "issue_id": "1234567223a4eaefffbe9b2f59bb933b",
    "release": "v1.2.3"
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [Data](https://docs.byteplus.com/en/docs/299/68002#data) |\- |JavaScript error stack. |
|error_msg |String |\- |Error message. It is empty if the request succeeds. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### Data

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|stack |Object of [Stack](https://docs.byteplus.com/en/docs/299/68002#stack) |\- |JavaScript error stack. |

### Stack

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|values |Array of [Values](https://docs.byteplus.com/en/docs/299/68002#values) |\- |JavaScript error stack. |

### Values

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|raw_stacktrace |Object of [RawStacktrace](https://docs.byteplus.com/en/docs/299/68002#rawstacktrace) |\- |Stack of parsed JS errors. |
|stacktrace |Object of [Stacktrace](https://docs.byteplus.com/en/docs/299/68002#stacktrace) |\- |Stack of unparsed JS errors. |

### RawStacktrace

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|frames |Array of [Frames](https://docs.byteplus.com/en/docs/299/68002#frames) |\- |JavaScript error stack frame. |

### Stacktrace

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|frames |Array of [Frames](https://docs.byteplus.com/en/docs/299/68002#frames) |\- |JavaScript error stack frame. |

### Frames

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|colno |Long |1 |Column number. |
|lineno |Long |1 |Line number. |
|context_line |String |\- |The code for the corresponding line. |
|filename |String |12345.js |Corresponding file name. |
|function |String |x |Function name for the corresponding line. |
|release |String |v1.2.3 |Version. |
|post_context |Array of String |[] |The next 5 lines of code. |
|pre_context |Array of String |[] |The preceding 5 lines of code. |

## Sample response

```JSON
{
    "data": {
        "stack": {
            "values": [
                {
                    "raw_stacktrace": {
                        "frames": [
                            {
                                "filename": "12345.js",
                                "colno": 1,
                                "context_line": "",
                                "pre_context": [

                                ],
                                "release": "v1.2.3",
                                "lineno": 1,
                                "function": "x",
                                "in_app": false,
                                "post_context": [

                                ]
                            }
                        ]
                    },
                    "stacktrace": {
                        "frames": [
                            {
                                "post_context": [

                                ],
                                "pre_context": [

                                ],
                                "colno": 1,
                                "filename": "12345.js",
                                "release": "v1.2.3",
                                "context_line": "",
                                "lineno": 1,
                                "function": "x",
                                "in_app": false
                            }
                        ]
                    }
                }
            ]
        }
    },
    "error_msg": "",
    "error_no": 0
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.

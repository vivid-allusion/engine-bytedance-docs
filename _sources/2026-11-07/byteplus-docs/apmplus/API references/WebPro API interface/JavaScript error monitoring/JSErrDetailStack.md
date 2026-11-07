---
title: "JSErrDetailStack"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/JSErrDetailStack"
---

Get JavaScript error stack traces.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable endpoint based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=JSErrDetailStack&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |JSErrDetailStack |The API name. The API name is `JSErrDetailStack`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|common |Object of [CommonParams](https://docs.byteplus.com/en/docs/299/67952#commonparams) |Yes |\- |Public parameters. |
|issue_id |String |Yes |1234567223a4eaefffbe9b2f59bb933b |JavaScript error aggregation ID. |
|release |String |No |v1.2.3 |Version where the JavaScript error occurred. |

### CommonParams

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |Yes |12345 |Application ID. |
|site_type |String |Yes |web |Site type. |
|env |String |Yes |online |Environment. An empty string ("") indicates all environments. |
|os |String |No |webpro |Service type. Available values are **webpro**, **app**, and **minipro**. |
|user |String |No |test_user |Username. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=JSErrDetailStack&Version=2022-10-12
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
|data |Object of [JSErrStackDetail](https://docs.byteplus.com/en/docs/299/67952#jserrstackdetail) |\- |JavaScript error stack. |
|error_msg |String |\- |Error message. If the request was successful, this field is empty. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### JSErrStackDetail

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|stack |Object of [StackData](https://docs.byteplus.com/en/docs/299/67952#stackdata) |\- |JavaScript error stack. |

### StackData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|values |Array of [StackItem](https://docs.byteplus.com/en/docs/299/67952#stackitem) |\- |JavaScript error stack. |

### StackItem

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|stacktrace |Object of [StackTraceData](https://docs.byteplus.com/en/docs/299/67952#stacktracedata) |\- |Stack of unparsed JS errors. |
|raw_stacktrace |Object of [StackTraceData](https://docs.byteplus.com/en/docs/299/67952#stacktracedata) |\- |Stack of parsed JS errors. |

### StackTraceData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|frames |Array of [StackFrame](https://docs.byteplus.com/en/docs/299/67952#stackframe) |\- |JS error stack frame. |

### StackFrame

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|colno |Long |1 |Column number. |
|lineno |Long |1 |The line number. |
|release |String |v1.2.3 |Version. |
|filename |String |12345.js |Corresponding file name. |
|function |String |x |Function name for the corresponding line. |
|pre_context |Array of String |[] |The preceding 5 lines of code. |
|post_context |Array of String |[] |The next 5 lines of code. |

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
                                "pre_context": [],
                                "release": "v1.2.3",
                                "lineno": 1,
                                "function": "x",
                                "in_app": false,
                                "post_context": []
                            }
                        ]
                    },
                    "stacktrace": {
                        "frames": [
                            {
                                "post_context": [],
                                "pre_context": [],
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

No error codes are specific to this API. If the API call returns an error, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.

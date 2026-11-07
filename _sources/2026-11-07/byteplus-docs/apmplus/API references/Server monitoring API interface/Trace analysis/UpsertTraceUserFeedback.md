---
title: "UpsertTraceUserFeedback"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/UpsertTraceUserFeedback"
---

Adds or updates user feedback for a trace.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

Server\-side Monitoring has been deployed in multiple regions around the world to provide you with a more stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-server.cn\-beijing.byteplusapi.com.cn?Action=UpsertTraceUserFeedback&Version=2026\-01\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For details, see [Common parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |UpsertTraceUserFeedback |The API name. The API name is `UpsertTraceUserFeedback`. |
|Version |String |Yes |2026\-01\-01 |The API version. The API version is `2026-01-01`. |
|Workspace |String |Yes |default |Workspace. |
|TraceId |String |Yes |b7d963cxxxx30e7c5ddexxxx |The trace ID to query. |
|Value |String |Yes |LIKE |The rating value. Values:<br><br><br>* LIKE: Indicates a like.<br><br>* DISLIKE: Indicates a dislike. |
|Comment |String |No |\- |Description of the rating value. |
|UserId |String |Yes |user_10001 |The user ID. |
|UserName |String |Yes |zhansan |Username. |
|Metadata |JSON Map |No |\- |The user\-defined extension information, which is passed in as key\-value pairs. Each submission replaces all existing data. If this parameter is omitted, the existing data is cleared. |


<span id="metadata"></span>
### Metadata


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|key |String |Yes |source |The key name of the user\-defined information, which is used to identify the metadata field. |
|value |String |Yes |web |The key value of the user\-defined information, which is passed in together with the corresponding key name. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-server.cn-beijing.byteplusapi.com.cn?Action=UpsertTraceUserFeedback&Version=2026-01-01
{
    "Workspace": "default",
    "TraceId": "b7d963cxxxx30e7c5ddexxxx",
    "Value": "LIKE",
    "Comment": "-",
    "UserId": "user_10001",
    "UserName": "zhansan",
    "Metadata": {}
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

None.

<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "ResponseMetadata": {
        "Action": "UpsertTraceUserFeedback",
        "Region": "cn-north-1",
        "Service": "apmplus_server",
        "Version": "2026-01-01",
        "RequestId": "20230604110420****100232280022D31"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) codes for troubleshooting.

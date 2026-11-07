---
title: "JsBreadcrumbs"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/JsBreadcrumbs"
---

Get the breadcrumbs for a specific JavaScript error.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=JsBreadcrumbs&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |JsBreadcrumbs |The API name. The API name is `JsBreadcrumbs`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|common |Object of [CommonParams](https://docs.byteplus.com/en/docs/299/67945#commonparams) |Yes |\- |Public parameters. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/67945#timefilter) |Yes |\- |Time range. |
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
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=JsBreadcrumbs&Version=2022-10-12
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
|data |Array of [BreadCrumbs](https://docs.byteplus.com/en/docs/299/67945#breadcrumbs) |\- |Breadcrumbs for a specific JavaScript error. |
|error_msg |String |\- |Error message. It is empty if the request succeeds. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### BreadCrumbs

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |JSON Map |[status:400](status:400) |Event\-related metadata. |
|type |String |dom,http |Breadcrumb type. |
|level |String |error,warn |Event level. |
|message |String |xpath,keyvalue,url |Event description. |
|category |String |ui.click, ui.keypress \| post,get |Event category. |
|timestamp |Double |1668576271511 |The timestamp when the event occurred. |

### Data

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |\- |Event metadata key. |
|value |String | | |

## Sample response

```JSON
{
    "error_no": 0,
    "data": [
        {
            "event_id": "",
            "type": "dom,http",
            "timestamp": 1668576271511,
            "data": "<status:400>",
            "level": "error,warn",
            "category": "ui.click, ui.keypress | post,get",
            "message": "xpath,keyvalue,url"
        }
    ],
    "error_msg": ""
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.

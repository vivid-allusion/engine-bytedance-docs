---
title: "MiniProJsErrDetailReleaseList"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/MiniProJsErrDetailReleaseList"
---

Get the JavaScript error release information.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=MiniProJsErrDetailReleaseList&Version=2024\-03\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |MiniProJsErrDetailReleaseList |The name of the API action. The current API name is `MiniProJsErrDetailReleaseList`. |
|Version |String |Yes |2024\-03\-12 |The API version. The current API version is `2024-03-12`. |
|common |Object of [Common](https://docs.byteplus.com/en/docs/299/68004#common) |Yes |\- |Common parameters. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/68004#timefilter) |Yes |\- |Time range. |
|issue_id |String |Yes |2769ad7223a4eaefffbe9b2f59bb933b |JavaScript error aggregation ID. |

### Common

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |Yes |12345 |Application ID. |
|site_type |String |Yes |web |Site type. |
|env |String |Yes |online |Environment. An empty string "" indicates all. |
|os |String |No |minipro |Service type. Available values are **webpro**, **app**, and **minipro**. |
|user |String |No |test_user |Username. |

### TimeFilter

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|start_time |Integer |Yes |1665485413 |Start time, in seconds. |
|granularity |Integer |No |3600 |Aggregation granularity, in seconds. |
|end_time |Integer |Yes |1665744613 |End time, in seconds. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=MiniProJsErrDetailReleaseList&Version=2024-03-12
{
    "time_filter": {
        "start_time": 1711713122,
        "end_time": 1711972322,
        "granularity": 10800
    },
    "common": {
        "site_type": "wx",
        "env": "release",
        "aid": 392926
    },
    "issue_id": "733f3d3463ebf7c8c3fea026f47c2941",
    "env": "release"
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [Data](https://docs.byteplus.com/en/docs/299/68004#data) |\- |JavaScript error details. |
|error_msg |String |\- |Error message. Empty indicates success. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### Data

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|releases |Array of String |\- |List of versions where JavaScript errors occurred. |

## Sample response

```JSON
{
  "releases": [
    "1.0.81"
  ]
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.

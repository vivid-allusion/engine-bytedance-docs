---
title: "MiniProJsErrDetailStartEndInfo"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/MiniProJsErrDetailStartEndInfo"
---

Get the start and end events of JavaScript errors.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable endpoint based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=MiniProJsErrDetailStartEndInfo&Version=2024\-03\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |MiniProJsErrDetailStartEndInfo |The API name. The API name is `MiniProJsErrDetailStartEndInfo`. |
|Version |String |Yes |2024\-03\-12 |The API version. The current API version is `2024-03-12`. |
|common |Object of [Common](https://docs.byteplus.com/en/docs/299/68001#common) |Yes |\- |Common parameters. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/68001#timefilter) |Yes |\- |Time range. |
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
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=MiniProJsErrDetailStartEndInfo&Version=2024-03-12
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
    "issue_id": "733f3d3463ebf7c8c3fea026f47c2941"
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [Data](https://docs.byteplus.com/en/docs/299/68001#data) |\- |JavaScript error details. |
|error_msg |String |\- |Error message. An empty value indicates success. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### Data

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|min_crash_time |Long |1668561659926 |Occurrence time of the earliest JavaScript error within the selected time range. |
|max_crash_time |Long |1678561659926 |Occurrence time of the latest JavaScript error within the selected time range. |
|min_crash_release |String |v1.2.3 |Earliest version in which the JavaScript error occurred within the selected time range. |
|max_crash_release |String |v1.2.4 |Latest version in which the JavaScript error occurred within the selected time range. |
|min_crash_pid |String |pid_1 |The page on which the JavaScript error first occurred within the selected time range. |
|max_crash_pid |String |pid_2 |The page on which the JavaScript error last occurred within the selected time range. |

## Sample response

```JSON
{
  "err_detail": "",
  "data": {
    "min_crash_time": 1711713185355,
    "max_crash_time": 1711972265560,
    "min_crash_release": "1.0.81",
    "max_crash_release": "1.0.81",
    "min_crash_pid": "page monitor",
    "max_crash_pid": "page home"
  },
  "error_msg": "",
  "error_no": 0
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.

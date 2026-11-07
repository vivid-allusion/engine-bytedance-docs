---
title: "MiniProAlarmDistribution"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/MiniProAlarmDistribution"
---

Get the alert type distribution.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable endpoint based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=MiniProAlarmDistribution&Version=2024\-03\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |MiniProAlarmDistribution |The API name. The current API name is `MiniProAlarmDistribution`. |
|Version |String |Yes |2024\-03\-12 |The API version. The current API version is `2024-03-12`. |
|common |Object of [Common](https://docs.byteplus.com/en/docs/299/68014#common) |Yes |\- |Common parameters. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/68014#timefilter) |Yes |\- |Time range. |
|name_list |Array of String |No |11111 |Alert task name list. If this parameter is not specified, the alert history for all alert tasks is returned.`GetAlarmRuleList` interface to view the value. |
|level_list |Array of String |No |warning |Alert level list. All alert types are returned if this field is left empty.<br><br><br>* warning<br><br>* fatal |
|category_list |Array of String |No |pageview |Alert task type. If this parameter is not specified, the history alerts of all types are returned. Call the `GetAlarmMeta` interface to view the value. |

### Common

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |Yes |12345 |Application ID. |
|os |String |No |minipro |Service type. Values supported: **app**, **webpro**, **minipro**. |

### TimeFilter

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|start_time |Integer |Yes |1665849600 |Start time. |
|granularity |Integer |No |60 |Aggregation granularity. |
|end_time |Integer |Yes |1666011403 |End time. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=MiniProAlarmDistribution&Version=2024-03-12
{
    "common": {
        "aid": 12345,
        "os": "minipro"
    },
    "time_filter": {
        "start_time": 1665849600,
        "end_time": 1666011403,
        "granularity": 3600
    },
    "page_size": 10,
    "page_num": 1,
    "category_list": [
        "pageview"
    ],
    "name_list": [
        "111111111"
    ],
    "level_list": [
        "warning"
    ]
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Array of [Data](https://docs.byteplus.com/en/docs/299/68014#data) |\- |Returned data. |
|error_msg |String |\- |Error message. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### Data

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|category |String |pageview |Alert task type. |
|count |Long |1407 |Alert count for this type. |
|percent |Double |1 |Percentage of alerts of this type among all alerts. |

## Sample response

```JSON
{
    "err_detail":"",
    "data":"all-history_xxx-xxx.xlsx",
    "error_msg":"",
    "error_no":0
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.

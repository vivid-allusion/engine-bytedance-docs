---
title: "MiniProDownloadAlarmHistory"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/MiniProDownloadAlarmHistory"
---

Download alert history data.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable endpoint based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=MiniProDownloadAlarmHistory&Version=2024\-03\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |MiniProDownloadAlarmHistory |The API name. The current API name is `MiniProDownloadAlarmHistory`. |
|Version |String |Yes |2024\-03\-12 |The API version. The current API version is `2024-03-12`. |
|common |Object of [Common](https://docs.byteplus.com/en/docs/299/68023#common) |Yes |\- |Public parameters. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/68023#timefilter) |Yes |302 |Time range. |
|category_list |Array of String |No |pageview |Alert type. If this parameter is not specified, the alert history for all alert types is returned. Call the `GetAlarmMeta` API to view the value. |
|name_list |Array of String |No |11111 |Alert task name list. If this parameter is not specified, the alert history for all alert tasks is returned. Call the `GetAlarmRuleList` API to view available values. |
|level_list |Array of String |No |warning |Alert level list. All alert types are returned if this field is left empty.<br><br><br>* warning<br><br>* fatal |
|id |Long |No |302 |Alert task ID list. |
|page_size |Integer |No |10 |Number of items returned in the alert history list. |
|page_num |Integer |No |1 |Page number of the alert history list. |

### Common

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |Yes |12345 |Application ID. |
|os |String |No |minipro |Service type. Supported values are **app**, **webpro**, **minipro**. |

### TimeFilter

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|start_time |Integer |Yes |1665849600 |Start time. |
|granularity |Integer |No |60 |Aggregation granularity. |
|end_time |Integer |Yes |1666011403 |End time. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=MiniProDownloadAlarmHistory&Version=2024-03-12
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
|data |String |all\-history_xxx\-xxx.xlsx |Unique key for the file. |
|error_msg |String |\- |Error message. |
|error_no |Integer |0 |Error code. 0 indicates success. |

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

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.

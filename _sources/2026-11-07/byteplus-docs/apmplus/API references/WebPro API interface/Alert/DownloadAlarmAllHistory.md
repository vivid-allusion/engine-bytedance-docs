---
title: "DownloadAlarmAllHistory"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/DownloadAlarmAllHistory"
---

Download alert history.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable endpoint based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=DownloadAlarmAllHistory&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |DownloadAlarmAllHistory |The API name. The API name is `DownloadAlarmAllHistory`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|common |Object of [Common](https://docs.byteplus.com/en/docs/299/67928#common) |No |\- |Common parameters. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/67928#timefilter) |No |\- |Time range. |
|category_list |Array of String |No |pageview |Alert task type. If this parameter is not specified, the history alerts of all types are returned. Call the `GetAlarmMeta` API to view available values.. |
|name_list |Array of String |No |1111 |A list of alert task names. All alert histories are returned if this parameter is left empty. Call the `GetAlarmRuleList` API to view available values. |
|level_list |Array of String |No |warning |A list of alert levels. All alert types are returned if this field is left empty.<br><br><br>* warning<br><br>* fatal |
|page_size |Integer |No |30 |The number of items per page for a pagination query. Default value: 30. |
|page_num |Integer |No |1 |The page number for a pagination query. Default value: 1. |

### Common

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |No |12345 |Application ID. |
|os |String |No |webpro |Service type. |

### TimeFilter

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|start_time |Integer |No |1665849600 |Start time. |
|granularity |Integer |No |60 |Aggregation time granularity. Unit: s. |
|end_time |Integer |No |1666011403 |The end time. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=DownloadAlarmAllHistory&Version=2022-10-12
{
    "common":{
        "aid":12345,
        "os":"webpro"
    },
    "time_filter":{
        "start_time":1665849600,
        "end_time":1666011403,
        "granularity":3600
    },
    "page_size":10,
    "page_num":1,
    "category_list":[
        "pageview"
    ],
    "name_list":[
        "111111111"
    ],
    "level_list":[
        "warning"
    ]
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |String |\- |Response data. |
|error_msg |String |"" |Error message. An empty string `""` indicates success. |
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

No error codes are specific to this API. If the API call returns an error, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.

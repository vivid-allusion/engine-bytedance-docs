---
title: "MiniProAlarmEventMeta"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/MiniProAlarmEventMeta"
---

Get alert event name metrics.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable endpoint based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=MiniProAlarmEventMeta&Version=2024\-03\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |MiniProAlarmEventMeta |The API name. The API name is `MiniProAlarmEventMeta`. |
|Version |String |Yes |2024\-03\-12 |The API version. The current API version is `2024-03-12`. |
|common |Object of [Common](https://docs.byteplus.com/en/docs/299/68013#common) |Yes |\- |Common parameters. |

### Common

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |Yes |12345 |Application ID. |
|os |String |No |minipro |Service type. Supported values: **app**, **webpro**, **minipro**. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=MiniProAlarmEventMeta&Version=2024-03-12
{
    "common": {
        "aid": 12345,
        "os": "minipro"
    }
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [Data](https://docs.byteplus.com/en/docs/299/68013#data) |\- |Response data. |
|error_msg |String |\- |Error message. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### Data

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|event_meta_list |Array of [EventMetaList](https://docs.byteplus.com/en/docs/299/68013#eventmetalist) |\- |All supported alert types. |

### EventMetaList

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|label |String |basic\-custom |Alert type. |
|event_name |String |basic\-custom |Custom event name. |

## Sample response

```JSON
{
    "err_detail":"",
    "data":{
        "event_meta_list":[
            {
                "label":"basic-custom",
                "event_name":"basic-custom"
            },
            {
                "label":"custom-metrics",
                "event_name":"custom-metrics"
            }
        ]
    },
    "error_msg":"",
    "error_no":0
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.

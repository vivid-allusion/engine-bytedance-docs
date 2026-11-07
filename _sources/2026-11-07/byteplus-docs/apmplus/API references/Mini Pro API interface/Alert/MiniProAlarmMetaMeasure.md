---
title: "MiniProAlarmMetaMeasure"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/MiniProAlarmMetaMeasure"
---

Get detailed metrics of an event.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable endpoint based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=MiniProAlarmMetaMeasure&Version=2024\-03\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |MiniProAlarmMetaMeasure |The API name. The API name is `MiniProAlarmMetaMeasure`. |
|Version |String |Yes |2024\-03\-12 |The API version. The current API version is `2024-03-12`. |
|common |Object of [Common](https://docs.byteplus.com/en/docs/299/68015#common) |Yes |\- |Common parameters. |
|event_name |String |Yes |basic\-custo |Event name. Call the `GetAlarmEventMeta` API to view available values. |

### Common

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |Yes |12345 |Application ID. |
|os |String |No |webpro |Service type. Supported values: **app**, **webpro**, **minipro**. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=MiniProAlarmMetaMeasure&Version=2024-03-12
{
    "common": {
        "aid": 12345,
        "os": "minipro"
    },
    "event_name": "basic-custom"
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [Data](https://docs.byteplus.com/en/docs/299/68015#data) |\- |Response data. |
|error_msg |String |\- |Error message. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### Data

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|measure_meta_list |Array of [MeasureMetaList](https://docs.byteplus.com/en/docs/299/68015#measuremetalist) |\- |Alert metric list. |

### MeasureMetaList

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |\- |Unique key for alert type. |
|type |String |basic |Metric type. |
|label |String |basic\-custom/events |Metric. |
|measure_name |String |{"metric":"custom.count","event_dimension":"event_name","event_name":"basic\-custom"} |Alert metric name. |
|measure_meta_list |Array of [MeasureMetaList](https://docs.byteplus.com/en/docs/299/68015#measuremetalist) |\- |Alert metric metadata. |

## Sample response

```JSON
{
    "err_detail":"",
    "data":{
        "measure_meta_list":[
            {
                "key":"",
                "type":"basic",
                "label":"basic-custom/reporting volume ",
                "short_label":"",
                "measure_name":"{\"metric\":\"custom.count\",\"event_dimension\":\"event_name\",\"event_name\":\"basic-custom\"}",
                "measure_meta_list":[
                ],
                "comment":{
                    "link":"",
                    "comment":"",
                    "event_comment":"The reporting volume of the event basic-custom"
                },
                "event_name":"basic-custom",
                "unit":{
                    "unit_type":"",
                    "unit":""
                },
                "agg_func_list":[
                ]
            },
            {
                "key":"",
                "type":"basic",
                "label":"basic-custom/fruit/Distinct count",
                "short_label":"",
                "measure_name":"{\"metric\":\"custom.categories.uniq\",\"event_dimension\":\"event_name\",\"event_name\":\"basic-custom\",\"map_key\":\"fruit\"}",
                "measure_meta_list":[
                ],
                "comment":{
                    "link":"",
                    "comment":"",
                    "event_comment":"Distinct count of the category fruit for the event basic-custom"
                },
                "event_name":"basic-custom",
                "unit":{
                    "unit_type":"",
                    "unit":""
                },
                "agg_func_list":[
                ]
            }
        ]
    },
    "error_msg":"",
    "error_no":0
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.

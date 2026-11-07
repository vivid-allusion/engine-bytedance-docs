---
title: "GetAlarmEventMetaMetric"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAlarmEventMetaMetric"
---

Get the alert metrics for a specified custom event.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable endpoint based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetAlarmEventMetaMetric&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAlarmEventMetaMetric |The API name. The API name is `GetAlarmEventMetaMetric`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|common |Object of [Common](https://docs.byteplus.com/en/docs/299/67937#common) |No |\- |Common parameters. |
|event_name |String |No |basic\-custom |Event name. Call the `GetAlarmEventMeta` API to view available values. |

### Common

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |No |12345 |Application ID. |
|os |String |No |webpro |Service type. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetAlarmEventMetaMetric&Version=2022-10-12
{
    "common":{
        "aid":12345,
        "os":"webpro"
    },
    "event_name":"basic-custom"
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [Data](https://docs.byteplus.com/en/docs/299/67937#data) |\- |Response data. |
|error_msg |String |\- |Error message. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### Data

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|measure_meta_list |Array of [MeasureMetaList](https://docs.byteplus.com/en/docs/299/67937#measuremetalist) |\- |A list of alert metrics. |

### MeasureMetaList

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |\- |The unique key for the alert type. |
|type |String |basic |Metric type. |
|label |String |basic\-custom/report\-volume |Metric. |
|measure_name |String |{"metric":"custom.count","event_dimension":"event_name","event_name":"basic\-custom"} |Alert metric name. |
|measure_meta_list |Array of [MeasureMetaList](https://docs.byteplus.com/en/docs/299/67937#measuremetalist) |\- |Alert metric metadata. |

## Sample response

```JSON
{
    "err_detail":"",
    "data":{
        "measure_meta_list":[
            {
                "key":"",
                "type":"basic",
                "label":"basic-custom/Reporting volume",
                "short_label":"",
                "measure_name":"{\"metric\":\"custom.count\",\"event_dimension\":\"event_name\",\"event_name\":\"basic-custom\"}",
                "measure_meta_list":[
                ],
                "comment":{
                    "link":"",
                    "comment":"",
                    "event_comment":"Reporting volume of event basic-custom"
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
                "label":"basic-custom/fruit/Deduplicated count",
                "short_label":"",
                "measure_name":"{\"metric\":\"custom.categories.uniq\",\"event_dimension\":\"event_name\",\"event_name\":\"basic-custom\",\"map_key\":\"fruit\"}",
                "measure_meta_list":[
                ],
                "comment":{
                    "link":"",
                    "comment":"",
                    "event_comment":"Deduplicated count of category fruit for event basic-custom"
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

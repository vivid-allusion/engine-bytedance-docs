---
title: "GetAlarmMeta"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAlarmMeta"
---

Get alert metric metadata for all alert types.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable endpoint based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetAlarmMeta&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAlarmMeta |The API name. The API name is `GetAlarmMeta`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|common |Object of [CommonParams](https://docs.byteplus.com/en/docs/299/67926#commonparams) |No |\- |Common parameter. |

### CommonParams

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |Yes |12345 |Application ID. |
|site_type |String |Yes |web |Site type. |
|env |String |Yes |online |Environment. An empty string "" indicates all. |
|os |String |No |webpro |Service type. Available values are **webpro**, **app**, **minipro**. |
|user |String |No |test_user |Username. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetAlarmMeta&Version=2022-10-12
{
    "common":{
        "aid":12345,
        "os":"webpro"
    }
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [FlexMetaResponseData](https://docs.byteplus.com/en/docs/299/67926#flexmetaresponsedata) |\- |Response data. |
|error_msg |String |"" |Response data. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### FlexMetaResponseData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|measure_category_meta_list |Array of [FlexMeasureCategoryMetaItem](https://docs.byteplus.com/en/docs/299/67926#flexmeasurecategorymetaitem) |\- |Alert metadata returned. |

### FlexMeasureCategoryMetaItem

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |pageview |Unique key for alert type. |
|type |String |simple |Type.<br><br><br>* event: Indicates that event\-related APIs need to be called after an event is selected.<br><br>* simple: Indicates other fixed metrics. |
|label |String |User analysis |Alert type. |
|measure_meta_list |Array of [FlexMeasureMetaItem](https://docs.byteplus.com/en/docs/299/67926#flexmeasuremetaitem) |\- |Alert metrics for a specific alert type. |

### FlexMeasureMetaItem

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|type |String |basic |Indicates whether this metric has sub\-metrics.<br><br><br>* basic: There are no sub\-metrics<br><br>* group: There are sub\-metrics |
|label |String |PV |The metric name. |
|measure_name |String |pv_uv.count |Unique metric key. |

## Sample response

```JSON
{
    "err_detail":"",
    "data":{
        "measure_category_meta_list":[
            {
                "key":"pageview",
                "label":"user analysis",
                "type":"simple",
                "measure_meta_list":[
                    {
                        "key":"",
                        "type":"basic",
                        "label":"PV",
                        "short_label":"",
                        "measure_name":"pv_uv.count"
                    }
                ]
            },
            {
                "key":"performance",
                "label":"performance metric",
                "type":"simple",
                "measure_meta_list":[
                    {
                        "key":"",
                        "type":"group",
                        "label":"DomReady",
                        "short_label":"",
                        "measure_meta_list":[
                            {
                                "key":"",
                                "type":"basic",
                                "label":"DomReady/avg",
                                "short_label":"",
                                "measure_name":"browser_perf.dom_ready.avg"
                            }
                        ]
                    }
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

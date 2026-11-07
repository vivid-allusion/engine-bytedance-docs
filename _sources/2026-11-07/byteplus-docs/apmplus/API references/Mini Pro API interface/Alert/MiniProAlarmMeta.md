---
title: "MiniProAlarmMeta"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/MiniProAlarmMeta"
---

Get metadata such as the alert category and corresponding metrics.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable endpoint based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=MiniProAlarmMeta&Version=2024\-03\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |MiniProAlarmMeta |The API name. The name of the current API is `MiniProAlarmMeta`. |
|Version |String |Yes |2024\-03\-12 |The API version. The current API version is `2024-03-12`. |
|common |Object of [Common](https://docs.byteplus.com/en/docs/299/68019#common) |Yes |\- |Common parameters. |

### Common

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |Yes |12345 |Application ID. |
|os |String |No |minipro |Service type. <br><br>Supported values are **app**, **webpro**, and **minipro**. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=MiniProAlarmMeta&Version=2024-03-12
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
|data |Object of [Data](https://docs.byteplus.com/en/docs/299/68019#data) |\- |Response data. |
|error_msg |String |\- |Error message. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### Data

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|measure_category_meta_list |Array of [MeasureCategoryMetaList](https://docs.byteplus.com/en/docs/299/68019#measurecategorymetalist) |\- |All supported alert types. |

### MeasureCategoryMetaList

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |pageview |Unique key for the alert type. |
|label |String |User analysis |Alert type. |
|type |String |simple |Type. |
|measure_meta_list |Array of [MeasureMetaList](https://docs.byteplus.com/en/docs/299/68019#measuremetalist) |\- |Alert metrics under a specific alert type. |

### MeasureMetaList

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|type |String |basic |Whether there are sub\-metrics under this metric.<br><br><br>* basic: There are no sub\-metrics<br><br>* group: There are sub\-metrics |
|label |String |DomReady/average |The metric name. |
|measure_name |String |browser_perf.dom_ready.avg |Unique key for the metric. |

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

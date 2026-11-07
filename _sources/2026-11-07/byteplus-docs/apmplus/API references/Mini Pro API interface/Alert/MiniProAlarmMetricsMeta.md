---
title: "MiniProAlarmMetricsMeta"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/MiniProAlarmMetricsMeta"
---

Get filter, grouping, and attribution dimensions based on metrics.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable endpoint based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=MiniProAlarmMetricsMeta&Version=2024\-03\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |MiniProAlarmMetricsMeta |The API name. The API name is `MiniProAlarmMetricsMeta`. |
|Version |String |Yes |2024\-03\-12 |The API version. The current API version is `2024-03-12`. |
|common |Object of [Common](https://docs.byteplus.com/en/docs/299/68017#common) |Yes |\- |Common parameters. |
|measure |Object of [Measure](https://docs.byteplus.com/en/docs/299/68017#measure) |No |\- |Alert metric. |

### Common

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |Yes |12345 |Application ID. |
|os |String |No |minipro |Service type. Supported values: **app**, **webpro**, and **minipro**. |

### Measure

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|type |String |No |monomial |Metric type.<br><br><br>* monomial: Simple metric<br><br>* polynomial: Composite metric |
|raw_measure_list |Array of [RawMeasureList](https://docs.byteplus.com/en/docs/299/68017#rawmeasurelist) |No |\- |The set of all metrics. |
|formula |String |No |\- |Metric arithmetic formula. Optional when the metric type is the composite metric polynomial. |
|name |String |No |PV |The metric name.<br><br><br>* For a simple metric, the value is the metric name.<br><br>* For a composite metric, the value is the custom metric name. |

### RawMeasureList

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|measure_name |String |No |pv.uv.count |Simple metric key. Call the `GetAlarmMeta` and `GetAlarmEventMetaMetric` APIs to view available values. |
|filter_list |Array of [FilterList](https://docs.byteplus.com/en/docs/299/68017#filterlist) |No |\- |The filter condition. This parameter is optional when a simple metric in a composite metric has filtering conditions. |
|event_name |String |No |\- |Custom event key. Required when the metric is a custom event metric. |

### FilterList

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|op |String |No |in |Filter condition operator.<br><br><br>* in<br><br>* not_in<br><br>* regex<br><br>* not_regex |
|filter_name |String |No |browser_brand |Filter field. |
|values |Array of String |No |["Chrome"] |Filter criterion values. Call the `GetAlarmMetricCandidata` API to view available values. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=MiniProAlarmMetricsMeta&Version=2024-03-12
{
    "measure": {
        "type": "monomial",
        "raw_measure_list": [
            {
                "measure_name": "pv_uv.count",
                "event_name": "",
                "filter_list": [
                    {
                        "filter_name": "browser_brand",
                        "values": [
                            "Chrome"
                        ],
                        "op": "in"
                    }
                ]
            }
        ],
        "formula": "",
        "name": "PV",
        "unit": {
            "unit_type": "",
            "unit": ""
        }
    },
    "common": {
        "aid": 12345,
        "os": "minipro"
    }
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [Data](https://docs.byteplus.com/en/docs/299/68017#data) |\- |Returned data. |
|error_msg |String |\- |Error message. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### Data

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|filter_meta_list |Array of [FilterMetaList](https://docs.byteplus.com/en/docs/299/68017#filtermetalist) |\- |Supported filter conditions. |
|group_meta_list |Array of [GroupMetaList](https://docs.byteplus.com/en/docs/299/68017#groupmetalist) |\- |Supported grouping dimensions. |
|attribution_dimension_list |Array of [AttributionDimensionList](https://docs.byteplus.com/en/docs/299/68017#attributiondimensionlist) |\- |Supported attribution dimensions. |

### FilterMetaList

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|label |String |pid |Name of the filter condition. |
|filter_name |String |pid |The unique key of the filter condition. |
|filter_type |String |regex |The type of the filter condition. |

### GroupMetaList

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|label |String |work_country |Grouping dimension. |
|group_by_name |String |{"dimension":"context","map_key":"work_country"} |The unique key of the grouping dimension. |
|related_measure_name |Array of String |JS error/pv |The determination based on the grouping dimension. |

### AttributionDimensionList

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|label |String |pid |Name of the attribution dimension. |
|group_by_name |String |pid |The unique key of the attribution dimension. |

## Sample response

```JSON
{
    "err_detail":"",
    "data":{
        "filter_meta_list":[
            {
                "label":"pid",
                "filter_name":"pid",
                "filter_type":"regex"
            },
            {
                "label":"work_country",
                "filter_name":"{\"dimension\":\"context\",\"map_key\":\"work_country\"}",
                "filter_type":"regex"
            }
        ],
        "group_meta_list":[
            {
                "label":"pid",
                "group_by_name":"pid"
            },
            {
                "label":"work_country",
                "group_by_name":"{\"dimension\":\"context\",\"map_key\":\"work_country\"}",
                "related_measure_name":[
                    "jserror/pv"
                ],
                "comment":{
                    "link":"",
                    "comment":"",
                    "event_comment":""
                }
            }
        ],
        "attribution_dimension_list":[
            {
                "label":"pid",
                "group_by_name":"pid"
            }
        ],
        "measure_type":""
    },
    "error_msg":"",
    "error_no":0
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.

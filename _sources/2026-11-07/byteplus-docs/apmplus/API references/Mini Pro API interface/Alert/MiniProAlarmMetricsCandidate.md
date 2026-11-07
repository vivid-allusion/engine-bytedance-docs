---
title: "MiniProAlarmMetricsCandidate"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/MiniProAlarmMetricsCandidate"
---

Get the available values of specific filter criteria under the specified alert metric.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=MiniProAlarmMetricsCandidate&Version=2024\-03\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |MiniProAlarmMetricsCandidate |The API name. The current API name is `MiniProAlarmMetricsCandidate`. |
|Version |String |Yes |2024\-03\-12 |The API version. The current API version is `2024-03-12`. |
|common |Object of [Common](https://docs.byteplus.com/en/docs/299/68022#common) |Yes |\- |Common parameters. |
|flex_param |Object of [FlexParam](https://docs.byteplus.com/en/docs/299/68022#flexparam) |Yes |\- |Alert metrics and filtering conditions. |

### Common

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |Yes |12345 |Application ID. |
|os |String |No |minipro |Service type. Supported values: **app**, **webpro**, **minipro**. |

### FlexParam

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|measure_list |Array of [MeasureList](https://docs.byteplus.com/en/docs/299/68022#measurelist) |No |\- |Alert metric list. Call the `GetAlarmMeta` and `GetAlarmEventMetaMetric` APIs to view the values. |
|filter_name |String |No |browser_brand |The key of the filter condition. Call the `GetAlarmMetricRelatedMeta` API to view the values. |

### MeasureList

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|type |String |No |monomial |Metric type.<br><br><br>* monomial: Simple metric<br><br>* polynomial: Composite metric |
|raw_measure_list |Array of [RawMeasureList](https://docs.byteplus.com/en/docs/299/68022#rawmeasurelist) |No |\- |The set of all metrics. |
|formula |String |No |\- |Metric arithmetic formula.<br><br>Optional when the metric type is the composite metric polynomial. |
|name |String |No |PV |The metric name.<br><br><br>* For a simple metric, the value is the metric name.<br><br>* For a composite metric, the value is the custom metric name. |

### RawMeasureList

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|measure_name |String |No |pv_uv.count |Simple metric key. Call the `GetAlarmMeta` and `GetAlarmEventMetaMetric` APIs to view the values. |
|filter_list |Array of [FilterList](https://docs.byteplus.com/en/docs/299/68022#filterlist) |No |\- |The filter condition. This parameter is optional when a simple metric in a composite metric has filtering conditions. |
|event_name |String |No |\- |Custom event key. Required when the metric is a custom event metric. |

### FilterList

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|op |String |No |in |Filter condition operator.<br><br><br>* in<br><br>* not_in<br><br>* regex<br><br>* not_regex |
|filter_name |String |No |browser_brand |Filter field. Call the `GetAlarmEventMetaMetric` API to view available values. |
|values |Array of String |No |["Chrome"] |Filter criterion values. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=MiniProAlarmMetricsCandidate&Version=2024-03-12
{
    "flex_param": {
        "filter_name": "browser_brand",
        "measure_list": [
            {
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
                "name": "PV"
            }
        ]
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
|data |Object of [Data](https://docs.byteplus.com/en/docs/299/68022#data) |\- |Returned data. |
|error_msg |String |\- |Error message. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### Data

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|candidate_list |Array of [CandidateList](https://docs.byteplus.com/en/docs/299/68022#candidatelist) |\- |List of available values for filter criteria. |

### CandidateList

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|label |String |Chrome |The filter condition. |
|value |String |Chrome |Available values for filter criteria. |

## Sample response

```JSON
{
    "err_detail":"",
    "data":{
        "candidate_list":[
            {
                "label":"Chrome",
                "value":"Chrome"
            },
            {
                "label":"Chrome Mobile iOS",
                "value":"Chrome Mobile iOS"
            }
        ]
    },
    "error_msg":"",
    "error_no":0
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.

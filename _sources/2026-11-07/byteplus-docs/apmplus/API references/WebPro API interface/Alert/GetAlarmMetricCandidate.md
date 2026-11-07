---
title: "GetAlarmMetricCandidate"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAlarmMetricCandidate"
---

Get the available values of a specific filtering condition for the specified alert metric.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetAlarmMetricCandidate&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAlarmMetricCandidate |The API name. The API name is `GetAlarmMetricCandidate`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|common |Object of [Common](https://docs.byteplus.com/en/docs/299/67934#common) |No |\- |Common parameters. |
|flex_param |Object of [FlexParam](https://docs.byteplus.com/en/docs/299/67934#flexparam) |No |\- |Alert metrics and filtering conditions. |

### Common

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |No |12345 |Application ID. |
|os |String |No |webpro |Service type. |

### FlexParam

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|measure_list |Array of [MeasureList](https://docs.byteplus.com/en/docs/299/67934#measurelist) |No |\- |A list of alert metrics. Call the `GetAlarmMeta` and `GetAlarmEventMetaMetric` APIs to view the values. |
|filter_name |String |No |browser_brand |The key of the filtering condition. Call the `GetAlarmMetricRelatedMeta` API to view available values. |

### MeasureList

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|type |String |No |monomial |Metric type.<br><br><br>* monomial: Simple metric<br><br>* polynomial: Composite metric |
|raw_measure_list |Array of [RawMeasureList](https://docs.byteplus.com/en/docs/299/67934#rawmeasurelist) |No |\- |A list of all metrics. |
|formula |String |No |\- |The arithmetic formula for the metric.<br><br>This parameter is optional when the metric type is polynomial. |
|name |String |No |PV |The metric name.<br><br><br>* When the metric is a simple metric, it is the metric name.<br><br>* When the metric is a composite metric, it is the custom metric name. |

### RawMeasureList

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|measure_name |String |No |pv_uv.count |Simple metric key. Call the `GetAlarmMeta` and `GetAlarmEventMetaMetric` APIs to view the values. |
|filter_list |Array of [FilterList](https://docs.byteplus.com/en/docs/299/67934#filterlist) |No |\- |Custom event key. Required when the metric is a custom event metric. |
|event_name |String |No |\- |The filtering condition. This parameter is optional when a simple metric in a composite metric has filtering conditions. |

### FilterList

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|op |String |No |in |Filtering condition operator. Supported values include in, not_in, regex, and not_regex. |
|filter_name |String |No |browser_brand |Filter field. Call the `GetAlarmEventMetaMetric` API to view available values. |
|values |Array of String |No |["Chrome"] |Filtering condition values. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetAlarmMetricCandidate&Version=2022-10-12
{
    "flex_param":{
        "filter_name":"browser_brand",
        "measure_list":[
            {
                "type":"monomial",
                "raw_measure_list":[
                    {
                        "measure_name":"pv_uv.count",
                        "event_name":"",
                        "filter_list":[
                            {
                                "filter_name":"browser_brand",
                                "values":[
                                    "Chrome"
                                ],
                                "op":"in"
                            }
                        ]
                    }
                ],
                "formula":"",
                "name":"PV"
            }
        ]
    },
    "common":{
        "aid":12345,
        "os":"webpro"
    }
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [Data](https://docs.byteplus.com/en/docs/299/67934#data) |\- |Response data. |
|error_msg |String |\- |Error message. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### Data

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|candidate_list |Array of [CandidateList](https://docs.byteplus.com/en/docs/299/67934#candidatelist) |\- |A list of available values for filtering conditions. |

### CandidateList

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|label |String |Chrome |The filter condition. |
|value |String |Chrome |Available value for the filtering condition. |

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

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.

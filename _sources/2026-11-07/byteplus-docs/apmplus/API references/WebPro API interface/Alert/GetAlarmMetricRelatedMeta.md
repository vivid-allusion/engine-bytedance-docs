---
title: "GetAlarmMetricRelatedMeta"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAlarmMetricRelatedMeta"
---

Get the filtering conditions, grouping dimensions, and attribution dimensions supported by the specified metric.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetAlarmMetricRelatedMeta&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAlarmMetricRelatedMeta |The API name. The current API name is `GetAlarmMetricRelatedMeta`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|common |Object of [Common](https://docs.byteplus.com/en/docs/299/67930#common) |No |\- |Common parameters. |
|measure |Object of [Measure](https://docs.byteplus.com/en/docs/299/67930#measure) |No |\- |Alert metric. |

### Common

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |No |12345 |Application ID. |
|os |String |No |webpro |Service type. |

### Measure

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|type |String |No |monomial |Metric type.<br><br><br>* monomial: Simple metric<br><br>* polynomial: Composite metric |
|raw_measure_list |Array of [RawMeasureList](https://docs.byteplus.com/en/docs/299/67930#rawmeasurelist) |No |\- |A list of all metrics. |
|formula |String |No |\- |The arithmetic expression for the metric. This parameter is optional when the metric type is **polynomial**. |
|name |String |No |PV |The metric name.<br><br><br>* When the metric is a simple metric, it is the metric name.<br><br>* When the metric is a composite metric, it is the custom metric name. |

### RawMeasureList

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|measure_name |String |No |pv_uv.count |Simple metric key. Call the `GetAlarmMeta` and `GetAlarmEventMetaMetric` APIs to view the values. |
|filter_list |Array of [FilterList](https://docs.byteplus.com/en/docs/299/67930#filterlist) |No |\- |The filter condition. This parameter is optional when the metric type is polynomial or filter conditions are specified for a single simple metric. |
|event_name |String |No |\- |Custom event key. This parameter is optional when the metric is a custom event metric. |

### FilterList

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|op |String |No |in |Filtering condition operator. Supported values include in, not_in, regex, and not_regex. |
|filter_name |String |No |browser_brand |Filter field. |
|values |Array of String |No |["Chrome"] |Filtering condition values. Call the `GetAlarmMetricCandidate` API to query values. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetAlarmMetricRelatedMeta&Version=2022-10-12
{
    "measure":{
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
        "name":"PV",
        "unit":{
            "unit_type":"",
            "unit":""
        }
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
|data |Object of [Data](https://docs.byteplus.com/en/docs/299/67930#data) |\- |Response data. |
|error_msg |String |\- |Error message. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### Data

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|filter_meta_list |Array of [FilterMetaList](https://docs.byteplus.com/en/docs/299/67930#filtermetalist) |\- |Supported filtering conditions. |
|group_meta_list |Array of [GroupMetaList](https://docs.byteplus.com/en/docs/299/67930#groupmetalist) |\- |Supported grouping dimensions. |
|attribution_dimension_list |Array of [AttributionDimensionList](https://docs.byteplus.com/en/docs/299/67930#attributiondimensionlist) |\- |Supported attribution dimensions. |

### FilterMetaList

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|label |String |pid |Name of the filtering condition. |
|filter_name |String |pid |The unique key of the filtering condition. |
|filter_type |String |regex |The type of the filter condition. |

### GroupMetaList

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|label |String |work_country |Grouping dimension. |
|group_by_name |String |{"dimension":"context","map_key":"work_country"} |The unique key for the grouping dimension. |
|related_measure_name |Array of String |js error/pv |The names of the metrics related to the grouping dimension. |

### AttributionDimensionList

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|label |String |pid |Name of attribution dimension. |
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
                    "js error/pv"
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

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.

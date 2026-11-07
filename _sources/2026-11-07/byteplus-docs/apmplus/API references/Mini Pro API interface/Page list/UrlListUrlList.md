---
title: "UrlListUrlList"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/UrlListUrlList"
---

View page list metric data.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable endpoint based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=MiniproUrlListUrlList&Version=2024\-03\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |MiniproUrlListUrlList |The API name. The current API name is `MiniproUrlListUrlList`. |
|Version |String |Yes |2024\-03\-12 |The API version. The current API version is `2024-03-12`. |
|common |Object of [Common](https://docs.byteplus.com/en/docs/299/120625#common) |No |\- |Common parameters. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/120625#timefilter) |No |\- |Time filter. |
|filter_conditions |Object of [FilterConditions](https://docs.byteplus.com/en/docs/299/120625#filterconditions) |No |\- |The filter condition. |
|page_num |Integer |No |1 |Number of pages when paginating. |
|page_size |Integer |No |10 |Number of items per page when paginating. |
|order |String |No |asc |Sort order.<br><br><br>* asc: Ascending order<br><br>* desc: Descending order |
|order_by_metric |String |No |count |Sort field.<br><br><br>* count: By absolute number<br><br>* user: By user count |
|search_text |String |No |test |Fuzzy search text. |
|metric_list |Array of [MetricList](https://docs.byteplus.com/en/docs/299/120625#metriclist) |No |\- |Metric list. It can be obtained via the `UrlListOverviewMetrics` API. |

### Common

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |Yes |392926 |The app ID. |

### TimeFilter

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|start_time |Integer |Yes |1762088409 |Start time. |
|granularity |Integer |No |10800 |Time granularity. |
|end_time |Integer |Yes |1762347609 |End time. |

### FilterConditions

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|type |String |Yes |and |The type of the filter condition.<br><br><br>* and: The conditions in children are in an "AND" relationship.<br><br>* rule: (Default) The current condition is an atomic condition. |
|field |String |No |pid |Condition field. |
|op |String |No |in |Condition operators. Available values include: eq, neq, lt, lte, gt, gte, in, not<br><br>_in, regex, not_regex. |
|values |Array of String |No |["test"] |Values of the filter condition. The set of available values can be obtained via the `MiniProGetFieldValues` API. |
|children |Array of |No |\- |Sub\-parameters of the filter condition. They are required only when the type value is `and`. The children parameter can contain nested conditions but cannot coexist with op, field, or values. |

### MetricList

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|description |String |No |PV |Metric description. |
|groupKey |String |No |base |Metric aggregation key. |
|groupName |String |No |User analysis |Metric aggregation name. |
|name |String |No |pv_count |The metric name. |
|isDefault |Boolean |No |true |Whether it is a default metric. |
|type |String |No |number |Metric type. |
|unit |String |No |ms |Unit. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=MiniproUrlListUrlList&Version=2024-03-12
{
    "time_filter": {
        "start_time": 1762140190,
        "end_time": 1762399390,
        "granularity": 10800
    },
    "common": {
        "aid": 392926,
    },
    "page_num": 1,
    "page_size": 10,
    "order": "asc",
    "order_by_metric": "pv_count",
    "search_text": "",
    "metric_list": [
        {
            "description": "PV",
            "groupKey": "base",
            "groupName": "User analysis",
            "name": "pv_count",
            "isDefault": true,
            "type": "number",
            "unit": ""
        },
        {
            "description": "Request success rate",
            "groupKey": "http",
            "groupName": "Request data",
            "name": "success_request_count_rate",
            "isDefault": true,
            "type": "rate",
            "unit": "%"
        }
    ],
    "top_pids": []
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [Data](https://docs.byteplus.com/en/docs/299/120625#data) |\- |Returned data. |
|error_msg |String |"" |Error message. |
|error_no |Integer |0 |Error code. |

### Data

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|table_list |Array of [TableList](https://docs.byteplus.com/en/docs/299/120625#tablelist) |\- |Table data. |
|count |Integer |17 |Total number of records in the table. |
|summary_metric |JSON Map |\- |Aggregated statistical metric data. |

### TableList

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|metric_map |JSON Map |\- |Metric details. |
|name |String |PID |Data row header name. |
|link |String |page one |Data row header value. |
|onTop |Boolean |true |Defaults to false. The value is true if the page is pinned to the top by the user. |

### SummaryMetric

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |js_error_error_count |Field name of the aggregated statistical metric. |
|value |Object of [Value](https://docs.byteplus.com/en/docs/299/120625#value) |\- |Aggregated statistical metric field value. |

### MetricMap

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |js_error_error_count |Metric field name. |
|value |Object of [Value](https://docs.byteplus.com/en/docs/299/120625#value) |\- |Metric field value. |

### Value

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|change |Double |0.0068 |Data change rate. |
|value |Double |2807 |Current value. |
|positive |Boolean |true |"true" indicates growth. "false" indicates decline. |

## Sample response

```JSON
{
    "err_detail": "",
    "data": {
        "table_list": [
            {
                "metric_map": {
                    "js_error_error_count": {
                        "change": 0,
                        "value": 0,
                        "positive": true,
                        "link": ""
                    },
            "uv_count": {
                "change": 0.0011,
                "value": 1761,
                "positive": true,
                "link": ""
            }
        }
    },
    "error_msg": "",
    "error_no": 0
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.

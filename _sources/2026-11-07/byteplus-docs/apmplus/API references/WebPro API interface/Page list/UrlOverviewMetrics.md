---
title: "UrlOverviewMetrics"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/UrlOverviewMetrics"
---

Obtain page\-related metrics.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=UrlOverviewMetrics&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |UrlOverviewMetrics |The API name. The API name is `UrlOverviewMetrics`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|common |Object of [CommonParams](https://docs.byteplus.com/en/docs/299/67986#commonparams) |Yes |\- |Common parameters. |

### CommonParams

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |Yes |12345 |Application ID. |
|site_type |String |Yes |web |Site type. |
|env |String |Yes |online |Environment. An empty string ("") indicates all environments. |
|os |String |No |webpro |Service type. Available values are **webpro**, **app**, and **minipro**. |
|user |String |No |test_user |Username. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=UrlOverviewMetrics&Version=2022-10-12
{
    "common": {
        "aid": 12345,
        "site_type": "web",
        "env": "online",
        "os": "webpro",
        "user": "test_user"
    }
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Array of [MetricList](https://docs.byteplus.com/en/docs/299/67986#metriclist) |\- |Page metrics. |
|error_msg |String |\- |Error message. An empty value indicates success. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### MetricList

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|name |String |js_error.count |Metric key. |
|type |String |number |Metric value type. It can be a numeric metric or a rate metric. |
|unit |String |ms |Metric value unit. |
|groupKey |String |js_error |Group key. |
|groupName |String |JS error |Group name. |
|isDefault |Boolean |true |Whether the metric is displayed by default. |
|description |String |PV |The metric name. |

## Sample response

```JSON
{
    "error_msg": "",
    "data": [
        {
            "type": "number",
            "groupKey": "js_error",
            "isDefault": true,
            "groupName": "JS error",
            "unit": "ms",
            "name": "js_error.count",
            "description": "PV"
        }
    ],
    "error_no": 0
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.

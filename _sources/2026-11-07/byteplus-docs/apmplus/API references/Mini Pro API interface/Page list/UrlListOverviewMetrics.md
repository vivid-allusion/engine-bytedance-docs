---
title: "UrlListOverviewMetrics"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/UrlListOverviewMetrics"
---

Query the available items for page list metrics.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=MiniproUrlListOverviewMetrics&Version=2024\-03\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |MiniproUrlListOverviewMetrics |The API name. The current API name is `MiniproUrlListOverviewMetrics`. |
|Version |String |Yes |2024\-03\-12 |The API version. The current API version is `2024-03-12`. |
|common |Object of [Common](https://docs.byteplus.com/en/docs/299/120626#common) |No |\- |Common parameters. |

### Common

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |Yes |392926 |The app ID. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=MiniproUrlListOverviewMetrics&Version=2024-03-12
{
    "common": {
        "aid": 392926,
    },
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Array of [Data](https://docs.byteplus.com/en/docs/299/120626#data) |\- |Returned data. |
|error_msg |String |"" |Error message. |
|error_no |Integer |0 |Error code. |

### Data

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|description |String |PV |Metric description. |
|groupKey |String |base |Metric aggregation key. |
|groupName |String |User analysis |Metric aggregation name. |
|name |String |pv_count |Metric name. |
|isDefault |Boolean |true |Whether it is a default metric. |
|type |String |number |Metric type. |
|unit |String |ms |Unit. |

## Sample response

```JSON
{
    "err_detail": "",
    "data": [
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
            "description": "UV",
            "groupKey": "base",
            "groupName": "User analysis",
            "name": "uv_count",
            "isDefault": true,
            "type": "number",
            "unit": ""
        }
    ],
    "error_msg": "",
    "error_no": 0
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.

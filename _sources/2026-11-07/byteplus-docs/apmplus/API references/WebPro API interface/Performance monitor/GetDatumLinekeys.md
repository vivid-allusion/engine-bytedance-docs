---
title: "GetDatumLinekeys"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetDatumLinekeys"
---

Get a performance monitor metric baseline.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable endpoint based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetDatumLinekeys&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetDatumLinekeys |The API name. The API name is `GetDatumLinekeys`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|common |Object of [CommonParams](https://docs.byteplus.com/en/docs/299/67959#commonparams) |Yes |\- |Common parameters. |

### CommonParams

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |Yes |12345 |Application ID. |
|site_type |String |Yes |web |Site type. |
|env |String |Yes |online |Environment. An empty string "" indicates all. |
|os |String |No |webpro |Service type. Available values are **webpro**, **app**, and **minipro**. |
|user |String |No |test_user |Username. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetDatumLinekeys&Version=2022-10-12
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
|data |Array of [DatumLine](https://docs.byteplus.com/en/docs/299/67959#datumline) |\- |Metric baseline. |
|error_msg |String |\- |Error message. Empty indicates success. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### DatumLine

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |browser_perf.cls.avg |Metric key. |
|name |String |Cumulative layout shift (CLS) |The metric name. |
|unit |String |ms |Metric value unit. |
|up_base_line |Double |2,000 |The maximum metric baseline. |
|down_base_line |Double |1,000 |The minimum metric baseline. |
|is_little_better |Boolean |true |Whether a smaller metric value is better. |

## Sample response

```JSON
{
    "error_msg": "",
    "data": [
        {
            "down_base_line": 1000,
            "is_little_better": true,
            "name": "Cumulative Layout Shift(CLS)",
            "ev_type": "",
            "unit": "ms",
            "num_type": "",
            "up_base_line": 2000,
            "key": "browser_perf.cls.avg"
        }
    ],
    "error_no": 0
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.

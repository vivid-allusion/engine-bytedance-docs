---
title: "SessionList"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/SessionList"
---

Get trace details for a specified session.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable endpoint based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=SessionList&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |SessionList |The API name. The API name is `SessionList`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|common |Object of [CommonParams](https://docs.byteplus.com/en/docs/299/67947#commonparams) |Yes |\- |Public parameters. |
|slardar_session_id |String |Yes |452551f8\-xxx\-9d50078ennb6 |session_id. It can be obtained via the DataList API. |
|timestamp |Integer |Yes |1668576681 |Session start timestamp. It can be obtained via the DataList API. |
|next_key |String |No |\- |Each request returns at most 200 records. If there are more than 200, a next_key is returned. Include the next_key in the next request to fetch the next 200 records starting from that position. |

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
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=SessionList&Version=2022-10-12
{
    "common": {
        "aid": 12345,
        "site_type": "web",
        "env": "online",
        "user": "test_user",
        "os": "webpro"
    },
    "slardar_session_id": "452551f8-xxx-9d50078ennb6",
    "timestamp": 1668576681,
    "next_key": ""
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [SessionListResponseData](https://docs.byteplus.com/en/docs/299/67947#sessionlistresponsedata) |\- |Trace details for the specified session. |
|error_msg |String |"" |Error message. Empty indicates success. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### SessionListResponseData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|next_key |String |\- |Each request returns at most 200 records. If there are more than 200, a next_key is returned. |
|table_list |Array of [DataListItem](https://docs.byteplus.com/en/docs/299/67947#datalistitem) |\- |Trace details. |

### DataListItem

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|json |String |\- |Raw reported JSON data. |
|ev_type |String |session |Report type. |
|metric_map |JSON Map |\- |Report details. |

### MetricMap

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |browser_brand |Key of the report parameter. |
|value |Object of [MetricData](https://docs.byteplus.com/en/docs/299/67947#metricdata) | | |

### MetricData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|unit |String |ms |Unit of the dimension value. |
|label |String |browser_brand |Dimension name. |
|value |String |Chrome |The reported value of a dimension. |
|groupKey |String |\- |Key of the dimension group. |
|groupName |String |\- |Name of the dimension group. |

## Sample response

```JSON
{
    "error_no": 0,
    "data": {
        "table_list": [
            {
                "metric_map": "{\"browser_brand\":{\"value\":\"Chrome\",\"label\":\"browser_brand\",\"groupKey\":\"\",\"groupName\":\"\"},\"fcp\":{\"value\":\"1109.6\",\"label\":\"FCP\",\"unit\":\"ms\",\"groupKey\":\"\",\"groupName\":\"\"}",
                "ev_type": "session",
                "json": ""
            }
        ],
        "next_key": ""
    },
    "error_msg": ""
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.

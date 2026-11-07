---
title: "MiniProJsErrDetailDistribution"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/MiniProJsErrDetailDistribution"
---

Get JavaScript error distribution details.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=MiniProJsErrDetailDistribution&Version=2024\-03\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |MiniProJsErrDetailDistribution |The API name. The current API name is `MiniProJsErrDetailDistribution`. |
|Version |String |Yes |2024\-03\-12 |The API version. The current API version is `2024-03-12`. |
|common |Object of [Common](https://docs.byteplus.com/en/docs/299/68000#common) |Yes |\- |Common parameters. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/68000#timefilter) |Yes |\- |Time range. |
|issue_id |String |Yes |2769ad7223a4eaefffbe9b2f59bb933b |JavaScript error aggregation ID. |

### Common

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|aid |Long |Yes |12345 |Application ID. |
|site_type |String |Yes |web |Site type. |
|env |String |Yes |online |Environment. An empty string ("") indicates all environments. |
|os |String |No |minipro |Service type. Available values are **webpro**, **app**, and **minipro**. |
|user |String |No |test_user |Username. |

### TimeFilter

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|start_time |Integer |Yes |1665485413 |Start time, in seconds. |
|granularity |Integer |No |3600 |Aggregation time granularity, in seconds. |
|end_time |Integer |Yes |1665744613 |End time, in seconds. |

## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=MiniProJsErrDetailDistribution&Version=2024-03-12
{
    "time_filter": {
        "start_time": 1711713122,
        "end_time": 1711972322,
        "granularity": 10800
    },
    "common": {
        "site_type": "wx",
        "env": "release",
        "aid": 392926
    },
    "issue_id": "733f3d3463ebf7c8c3fea026f47c2941",
    "dims": [
        "pid",
        "release"
    ]
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [Data](https://docs.byteplus.com/en/docs/299/68000#data) |\- |JavaScript error details. |
|error_msg |String |\- |Error message. Empty indicates success. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### Data

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|distributions |JSON Map |\- |Page distribution. |

### Distributions

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |/pages/index/index |The page path, which is the key of the distribution dimension. |
|value |Object of [Value](https://docs.byteplus.com/en/docs/299/68000#value) |\- |The distribution data for the corresponding page, including line chart and pie chart dimension data. |

### Value

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|fields |Array of [Fields](https://docs.byteplus.com/en/docs/299/68000#fields) |\- |Dimensions of the line chart or pie chart. len(fields) = len(source[i]). |
|source |Array of String |[["1668355200","js_error","0","0"]] |The set of data points in the trend chart. len(source) is the number of points in the line chart or the number of slices in the pie chart. |

### Fields

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |String |date |Dimension key. |
|dataType |String |string |Dimension type. |
|name |String |Date |Dimension name. |
|aggregate |String |\- |Aggregation method. |

## Sample response

```JSON
{
  "err_detail": "",
  "data": {
    "distributions": {
      "pid": {
        "fields": [
          {
            "id": "pid",
            "dataType": "string",
            "name": "pid"
          },
          {
            "id": "js_error.count",
            "dataType": "number",
            "name": "error count"
          }
        ],
        "source": [
          [
            "page overview",
            "415"
          ],
          [
            "page home",
            "460"
          ],
          [
            "page monitor",
            "437"
          ],
          [
            "page index",
            "445"
          ]
        ]
      },
      "release": {
        "fields": [
          {
            "id": "release",
            "dataType": "string",
            "name": "release"
          },
          {
            "id": "js_error.count",
            "dataType": "number",
            "name": "error count"
          }
        ],
        "source": [
          [
            "1.0.81",
            "1757"
          ]
        ]
      }
    }
  },
  "error_msg": "",
  "error_no": 0
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.

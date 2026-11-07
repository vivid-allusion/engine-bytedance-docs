---
title: "GetWebProNewErrorAlertTrend"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetWebProNewErrorAlertTrend"
---

Get the overview and trend chart of new error alerts.

## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.

* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetWebProNewErrorAlertTrend&Version=2022\-10\-12

## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetWebProNewErrorAlertTrend |The API name. The API name is `GetWebProNewErrorAlertTrend`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|time_filter |Object of [TimeFilter](https://docs.byteplus.com/en/docs/299/67996#timefilter) |No |\- |Time range. |
|id |Integer |No |1 |Alert ID. |
|common |Object of [CommonParams](https://docs.byteplus.com/en/docs/299/67996#commonparams) |Yes |\- |Common parameters. |

### TimeFilter

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|start_time |Integer |Yes |1665485413 |Start time, in seconds. |
|end_time |Integer |Yes |1665744613 |End time, in seconds. |
|granularity |Integer |No |3600 |Aggregation time granularity, in seconds. |

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
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetWebProNewErrorAlertTrend&Version=2022-10-12
{
  "common": {
    "aid": 1,
    "os": "webpro"
  },
  "time_filter": {
    "start_time": 1719936000,
    "end_time": 1720072371,
    "granularity": 3600
  },
  "id": 1
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [AlertTrendResponseData](https://docs.byteplus.com/en/docs/299/67996#alerttrendresponsedata) |\- |Response data. |
|error_msg |String |"" |Error message. An empty string `""` indicates success. |
|error_no |Integer |0 |Error code. 0 indicates success. |

### AlertTrendResponseData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|alert_trend |Object of [ChartData](https://docs.byteplus.com/en/docs/299/67996#chartdata) |\- |Alert trend details. |

### ChartData

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|fields |Array of [Field](https://docs.byteplus.com/en/docs/299/67996#field) |\- |Line chart/pie chart dimensions. len(fields)=len(source[i]). |
|source |Array of String |[["1668355200","js_error","0","0"]] |The set of specific points in the trend chart. len(source) is the number of points in the line chart or the number of blocks in the pie chart. |

### Field

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |String |date |Dimension key. |
|name |String |Date |Dimension name. |
|dataType |String |string |Dimension type. |
|aggregate |String |\- |Aggregation method. |

## Sample response

```JSON
{
  "alert_trend": {
    "fields": [
      {
        "id": "date",
        "dataType": "string",
        "name": "date"
      },
      {
        "id": "alarm_count",
        "dataType": "number",
        "name": "alert sum"
      }
    ],
    "source": [
      [
        "2024-07-03 00:00:00",
        "0"
      ],
      [
        "2024-07-04 13:00:00",
        "0"
      ]
    ]
  }
}
```

## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.

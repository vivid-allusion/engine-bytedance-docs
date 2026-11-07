---
title: "GetAppCustomTagValues"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAppCustomTagValues"
---

Get custom dimension values.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetAppCustomTagValues&Version=2022\-10\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAppCustomTagValues |The API name. The current API name is `GetAppCustomTagValues`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|aid |Integer |No |123456 |Application ID. |
|start_time |Integer |Yes |1665417600 |Start time. |
|end_time |Integer |Yes |1665504000 |The end time. |
|tag_key |String |Yes |anr_key |Tag key. |
|biz_type |String |Yes |crash |Metric type.<br><br><br>* crash: Crash<br><br>* crash_defend: Crash protection<br><br>* lag: Lag<br><br>* custom_exception: Custom exception<br><br>* battery: Battery metric<br><br>* battery_summary: Power consumption factors<br><br>* battery_trace: Anomaly trend |
|limit |Integer |No |100 |Number of data entries returned. Default: 100. |
|filters |Object of [Condition](https://docs.byteplus.com/en/docs/299/67866#condition) |No |\- |The filter condition. You can specify multiple key‑value pairs to filter data. |


<span id="condition"></span>
### Condition


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|op |String |No |in |The operator.<br><br><br>* gt: greater than<br><br>* gte: greater than or equal to<br><br>* lt: less than<br><br>* lte: less than or equal to<br><br>* eq: equal to<br><br>* neq: not equal to<br><br>* in: contains<br><br>* not_in: does not contain<br><br>* lk: Matches data that fits a specific pattern.<br><br>* nlk: Excludes data that fits a specific pattern. |
|type |String |No |expression |The type of the filter condition.<br><br><br>* expression: The current condition is an expression.<br><br>* and: The current condition is a compound expression, and multiple sub\-conditions are in an AND logical relationship.<br><br>* or: The current condition is a compound expression, and multiple sub\-conditions are in an OR logical relationship.<br><br>* map: The current condition is of map type. |
|value |String |No |123456 |The filter value. |
|values |Array of String |No |[123456] |The filter value. Multiple filter values are supported. |
|map_key |String |No |key_1 |The key of the map type. It is required when the type is set to map. |
|dimension |String |No |aid |The name of the condition. |
|sub_conditions |Array of [Condition](https://docs.byteplus.com/en/docs/299/67866#condition) |No |\- |The sub\-condition. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetAppCustomTagValues&Version=2022-10-12
{
  "tag_key": "anr_key",
  "aid": 12345,
  "biz_type": "crash",
  "limit": 100,
  "start_time": 1721012400,
  "end_time": 1721098907,
  "filters": {
    "type": "and",
    "sub_conditions": [
      {
        "dimension": "os",
        "op": "in",
        "type": "expression",
        "values": [
          "Android"
        ]
      }
    ]
  }
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Array of String |["123456", "1234567"] |Returned value. At most 100 entries. |
|error_msg |String |success |Error message. |
|error_no |Integer |0 |Error code. 0 indicates success. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
  "err_detail": "",
  "data": [
    "app_sleeping_long",
    "app_memleak",
    "app_deadlock_or_block"
  ],
  "error_msg": "",
  "error_no": 0
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.

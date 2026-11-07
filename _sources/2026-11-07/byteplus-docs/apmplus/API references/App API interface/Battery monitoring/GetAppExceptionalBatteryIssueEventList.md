---
title: "GetAppExceptionalBatteryIssueEventList"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAppExceptionalBatteryIssueEventList"
---

Get the app battery abnormal events.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetAppExceptionalBatteryIssueEventList&Version=2022\-10\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAppExceptionalBatteryIssueEventList |The API name. The current API name is `GetAppExceptionalBatteryIssueEventList`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|filters |Object of [Condition](https://docs.byteplus.com/en/docs/299/67904#condition) |No |\- |The filter condition. You can specify multiple key‑value pairs to filter data. |
|issue_id |String |No |issue_12345 |Issue ID. |
|is_new |Integer |No |1 |New issue.<br><br><br>* 1: New issue<br><br>* 0: Not a new issue |
|start_time |Integer |No |1619827200 |Query start time (Unix timestamp). |
|end_time |Integer |No |1619913600 |Query end time (Unix timestamp). |
|page_size |Integer |No |20 |Number of events displayed per page. |
|page_no |Integer |No |1 |Requested page number. |
|token |String |No |search_token |Search keyword. |


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
|sub_conditions |Array of [Condition](https://docs.byteplus.com/en/docs/299/67904#condition) |No |\- |The sub\-condition. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetAppExceptionalBatteryIssueEventList&Version=2022-10-12
{
    "filters": {
        "type": "and",
        "sub_conditions": [
            {
                "dimension": "apm_version",
                "type": "expression",
                "op": "in",
                "values": [
                    "1.4.5"
                ]
            },
            {
                "dimension": "device_model",
                "type": "expression",
                "op": "in",
                "values": [
                    "MI 5X"
                ]
            }
        ]
    },
    "issue_id": "issue_12345",
    "is_new": 1,
    "start_time": 1619827200,
    "end_time": 1619913600,
    "page_size": 20,
    "page_no": 1,
    "token": "search_token"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [BatteryTraceEventListData](https://docs.byteplus.com/en/docs/299/67904#batterytraceeventlistdata) |\- |Response data. |
|error_msg |String |success |Error message. |
|error_no |Integer |0 |Error code. |


<span id="batterytraceeventlistdata"></span>
### BatteryTraceEventListData


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|total |Integer |10 |The total number of list items. |
|result |Array of JSON Map |\- |List details. |


<span id="result"></span>
### Result


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |eventname |Key of the battery abnormal event. |
|value |String | | |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "data": {
        "total": 10,
        "result": []
    },
    "error_msg": "",
    "error_no": 0
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.

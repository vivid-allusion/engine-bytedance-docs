---
title: "GetAppHttpFieldValues"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAppHttpFieldValues"
---

Get available values for HTTP filter criteria for the app network.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetAppHttpFieldValues&Version=2025\-12\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Before you call this API, specify the required public request parameters (such as <code>x-app-ids</code>). Otherwise, the call fails.</div>



|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAppHttpFieldValues |The API name. The current API name is `GetAppHttpFieldValues`. |
|Version |String |Yes |2025\-12\-01 |The API version. The API version is `2025-12-01`. |
|StartTime |Integer |Yes |1617225600 |Timestamp of the query start time. |
|EndTime |Integer |Yes |1617312000 |Timestamp of the query end time. |
|Field |String |Yes |region |Name of the field to be aggregated or filtered. |
|Limit |Integer |Yes |10 |Limit on the number of records returned. |
|Filters |Object of [Condition](https://docs.byteplus.com/en/docs/299/67900#condition) |No |filters |The filter condition. You can specify multiple key‑value pairs to filter data. |
|Keyword |String |No |test |Fuzzy search keyword. |


<span id="condition"></span>
### Condition


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Op |String |No |in |The operator. Values:<br><br><br>* gt: greater than<br><br>* gte: greater than or equal to<br><br>* lt: less than<br><br>* lte: less than or equal to<br><br>* eq: equal to<br><br>* neq: not equal to<br><br>* in: contains<br><br>* not_in: does not contain<br><br>* lk: Matches data that fits a specific pattern.<br><br>* nlk: Excludes data that fits a specific pattern. |
|Type |String |No |expression |The type of the filter condition. Sample value:<br><br><br>* expression: The current condition is a single expression.<br><br>* and: The current condition is a compound expression, and the sub\-conditions in `SubConditions` are in a logical AND relationship.<br><br>* or: The current condition is a compound expression, and the sub\-conditions in `SubConditions` are in a logical OR relationship.<br><br>* map: The current condition is of the map type. |
|Value |String |No |123456 |The filter value. |
|MapKey |String |No |key_1 |The key of the map type.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when <code>type</code> is set to map.</div><br> |
|Values |Array of String |No |[123456] |The filter values. You can configure multiple values simultaneously. |
|Dimension |String |No |aid |The name of the condition. |
|SubConditions |Array of [Condition](https://docs.byteplus.com/en/docs/299/67900#condition) |No |\- |The sub\-condition. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetAppHttpFieldValues&Version=2025-12-01
{
    "StartTime": 1617225600,
    "EndTime": 1617312000,
    "Field": "region",
    "Limit": 10,
    "Filters": "filters",
    "Keyword": "test"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Label |String |Label 123 |Label used for frontend display. |
|Value |String |value123 |Value passed between the frontend and backend. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "ResponseMetadata": {
        "Action": "GetAppHttpFieldValues",
        "Region": "cn-north-1",
        "Service": "apmplus_openapi",
        "Version": "2025-12-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": [
        {
            "Label": "Label 123",
            "Value": "value123"
        }
    ],
    "error_msg": "fail",
    "error_no": "0",
    "data": [
        {
            "Label": "Label 123",
            "Value": "value123"
        }
    ]
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.

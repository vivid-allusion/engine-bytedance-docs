---
title: "ListSilencePolicies"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/ListSilencePolicies"
---

Obtain alert silence policies.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions

Vital Managed Service for Prometheus has been deployed in multiple regions worldwide, aiming to provide you with an experience of higher stability and lower latency. You can choose an access point that is the most optimal for the region of your services according to the [Service addresses](https://docs.byteplus.com/en/docs/vmp/Service_address) document.


* Request method: POST

* Request address: https://vmp.cn\-beijing.byteplusapi.com.cn?Action=ListSilencePolicies&Version=2021\-03\-03


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListSilencePolicies&serviceCode=vmp&version=2021-03-03&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListSilencePolicies |The name of the API. The API name is `ListSilencePolicies`. |
|Version |String |Yes |2021\-03\-03 |The API version. The API version is `2021-03-03`. |
|PageNumber |Long |No |1 |Current page number, minimum or default value is 1. |
|PageSize |Long |No |10 |Results per page. It is an integer from 0 to 100. The default number is 10. |
|Filter |Object of [SilencePolicyFilter](https://docs.byteplus.com/en/docs/88/31541#silencepolicyfilter) |No |\- |Filter condition. |
|SortBy |String |No |CreatedAt |Whether to perform query result sorting:<br><br><br>* The value `CreatedAt` indicates the results will be sorted. <br><br>* Absence of this parameter indicates no sorting. |
|SortOrder |String |No |Asc |Sorting order of query results:<br><br><br>* **Asc**: indicates ascending order sorting.<br><br>* **Desc**: indicates sorting in descending order. |


<span id="silencepolicyfilter"></span>
### SilencePolicyFilter


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Ids |Array of String |No |["e28ae750\-bbb8\-4ff4\-abf4\*\*\*"] |Exact query by IDs of alert silence policies. |
|Name |String |No |test |Fuzzy query by the names of alert silence policies. |
|Status |String |No |Disabled |Filter by statuses of alert silence policies. Available statuses:<br><br><br>* **Active**: Silence policies are within their effective period and are not disabled.<br><br>* **Disabled**: silence policies that are disabled.<br><br>* **Expired**: silence policies that are inactive due to expiration of active periods. Policies will not be active again unless the time periods are updated. |
|Sources |Array of String |No |General |Filter by sources of alert silence policies. Available sources:<br><br><br>* **General**: created via OpenAPI or console.<br><br>* **LarkBot**: created via the Feishu Application bot card. card. For more details, refer to [Receiving alerts by the Feishu application bot](https://docs.byteplus.com/en/docs/vmp/Receiving_alerting_notifications_through_Lark_application_robot). |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://vmp.cn-beijing.byteplusapi.com.cn?Action=ListSilencePolicies&Version=2021-03-03
Content-Type: application/json
{
    "PageNumber": 1,
    "PageSize": 10,
    "Filter": {
        "Ids": [
            "e28ae750-bbb8-4ff4-abf4***"
        ],
        "Name": "test",
        "Status": "Disabled",
        "Sources": [
            ""
        ]
    },
    "SortBy": "CreatedAt",
    "SortOrder": "Asc"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Total |Long |100 |Total number of query results. |
|Items |Array of [SilencePolicy](https://docs.byteplus.com/en/docs/88/31541#silencepolicy) |\- |A list of query results. |


<span id="silencepolicy"></span>
### SilencePolicy


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |e28ae750\-bbb8\-4ff4\-abf4\*\*\* |ID of alert silence policy. |
|Name |String |test |Name of alertlence policy. |
|Source |String |General |Source of alert silence policies. Available sources:<br><br><br>* **General**: created via OpenAPI or console.<br><br>* **LarkBot**: created via the Feishu Application bot card. |
|Status |String |Active |Status of alert silence policies. Available types:<br><br><br>* **Active**: Silence policies are within their effective period and are not disabled.<br><br>* **Disabled**: silence policies that are disabled.<br><br>* **Expired**: silence policies that are inactive due to expiration of active periods. Policies will not be active again unless the time periods are updated. |
|CreateTime |String |2020\-01\-01T00:00:00Z |The creation date of the alert silence policy. It is presented in RFC3339 format. |
|UpdateTime |String |2020\-01\-01T00:00:00Z |The update date of the alert silence policy. It is presented in RFC3339 format. |
|Description |String |This is a description |Description of alert silence policy. |
|AutoDeleteTime |String |2020\-01\-01T00:00:00Z |Automatic deletion time in the alert silence policy. |
|TimeRangeMatchers |Array of [TimeRangeMatcher](https://docs.byteplus.com/en/docs/88/31541#timerangematcher) |\- |Matching time in the alert silence policy. |
|MetricLabelMatchers |Array of [Matcher](https://docs.byteplus.com/en/docs/88/31541#matcher) |\- |Matching labels in alert silence policy. |


<span id="timerangematcher"></span>
### TimeRangeMatcher


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Date |String |2006\-01\-02 15:04~2006\-01\-03 14:04 |The time period of the alert silence. Used to activate alert silence within a specified time period. |
|Location |String |Asia/Shanghai |Time zone. |
|PeriodicDate |Object of [PeriodicDate](https://docs.byteplus.com/en/docs/88/31541#periodicdate) |\- |The alert silence period. Used to configure the alert silence that takes effect periodically. |


<span id="matcher"></span>
### Matcher


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Matchers |Array of [LabelMatcher](https://docs.byteplus.com/en/docs/88/31541#labelmatcher) | |Label matchers. Each LabelMatcher array can contain up to 24 items. |


<span id="periodicdate"></span>
### PeriodicDate


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Time |String |20:00~21:12 |Time period. You can specify multiple different time periods separated by commas (`,`), for example, `20:00~21:12,22:00~23:12`. You can configure up to 4 time periods. |
|Weekday |String |1,3,5 |Specific days within a week. You can specify multiple different time periods with commas (`,`). For example, `1,3,5` indicates Monday, Wednesday, and Friday of each week. 7 time periods can be configured at most. |
|DayOfMonth |String |2~3 |Specific days within a month. You can specify multiple different time periods separated by commas (`,`). For example, `2~3` indicates the 2nd and 3rd day of each month. 10 time periods can be configured at most. |


<span id="labelmatcher"></span>
### LabelMatcher


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Label |String |app |Label. |
|Value |String |test |Label Value. |
|Operator |String |Equal |The operator. Possible values:<br><br><br>* Equal: Equal<br><br>* NotEqual: Not equal<br><br>* RegexpEqual: Equal using a regular expression<br><br>* RegexpNotEqual: Not equal using a regular expression |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
HTTP/1.1: 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListSilencePolicies",
        "Version": "2021-03-03",
        "Service": "vmp",
        "Region": "cn-beijing"
    },
    "Result": {
        "Total": 100,
        "Items": [
            {
                "Id": "e28ae750-bbb8-4ff4-abf4***",
                "Name": "test",
                "Source": "General",
                "Status": "Active",
                "CreateTime": "2020-01-01T00:00:00Z",
                "UpdateTime": "2020-01-01T00:00:00Z",
                "Description": "Description",
                "AutoDeleteTime": "2020-01-01T00:00:00Z",
                "TimeRangeMatchers": [
                    {
                        "Date": "2006-01-02 15:04~2006-01-03 14:04",
                        "Location": "Asia/Shanghai",
                        "PeriodicDate": {
                            "Time": "20:00~21:12",
                            "Weekday": "1,3,5",
                            "DayOfMonth": "2~3"
                        }
                    }
                ],
                "MetricLabelMatchers": [
                    {
                        "Matchers": [
                            {
                                "Label": "app",
                                "Value": "test",
                                "Operator": "Equal"
                            }
                        ]
                    }
                ]
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The error codes for this API are listed in the table below. For a list of error codes for other APIs, see [Public error codes](https://docs.byteplus.com/en/docs/vmp/Common-error-codes).


|**HTTP status codes** |**Error code** |**Error message** |**Descriptions** |
|---|---|---|---|
|400 |InvalidParameter.{{parameter}} |The specified parameter {{parameter}} is invalid. |An invalid parameter was found. For example, an invalid workspace name was included in requests. |
|400 |MissingParameter.{{parameter}} |The required parameter {{parameter}} is missing. |A required parameter is missing. |
|403 |ProductUnsubscribed |You are not subscribed to VMP. Please go to the VMP console web page to subscribe to the service |The account has not subscribed to the VMP service. |

---
title: "CreateSilencePolicy"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/CreateSilencePolicy"
---

Create an alert silence policy.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions

Vital Managed Service for Prometheus has been deployed in multiple regions worldwide, aiming to provide you with an experience of higher stability and lower latency. You can choose an access point that is optimal for the region of your services according to the [Service addresses](https://docs.byteplus.com/en/docs/vmp/Service_address) document.


* Request method: POST

* Request address: https://vmp.cn\-beijing.byteplusapi.com.cn?Action=CreateSilencePolicy&Version=2021\-03\-03


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateSilencePolicy&serviceCode=vmp&version=2021-03-03&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |CreateSilencePolicy |The API name. The name of this API is `CreateSilencePolicy`. |
|Version |String |Yes |2021\-03\-03 |The API version. The API version is `2021-03-03`. |
|Name |String |Yes |alert\-silence\-demo |Name of alert silence policy.<br><br><br>* It is a string consisting of 1 to 128 characters.<br><br>* It can contain Chinese characters, letters, numbers, underscores, and hyphens. Starting with a number or underscore is not allowed.<br><br>* Duplicate names are not allowed in the same region. |
|Description |String |No |This is a description |Description of alert silence policy.<br><br><br>* It is a string consisting of 1 to 128 characters.<br><br>* Any utf\-8 characters can be used. |
|TimeRangeMatchers |Array of [TimeRangeMatcher](https://docs.byteplus.com/en/docs/88/31536#timerangematcher) |Yes |\- |Alert silence time. |
|MetricLabelMatchers |Array of [Matcher](https://docs.byteplus.com/en/docs/88/31536#matcher) |No | |Alert event label matchers. At most 32 items are allowed. Items follow an "OR" relationship.<br><br>Different LabelMatchers are evaluated using an "AND" relationship. |


<span id="timerangematcher"></span>
### TimeRangeMatcher


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Date |String |No |2006\-01\-02 15:04~2006\-01\-03 14:04 |The time period of the alert silence. Used to activate alert silence within a specified time period. |
|Location |String |Yes |Asia/Shanghai |Time zone |
|PeriodicDate |Object of [PeriodicDate](https://docs.byteplus.com/en/docs/88/31536#periodicdate) |No |\- |The alert silence period. Used to configure the alert silence that takes effect periodically. |


<span id="matcher"></span>
### Matcher


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Matchers |Array of [LabelMatcher](https://docs.byteplus.com/en/docs/88/31536#labelmatcher) |Yes | |Label matchers. Each LabelMatcher array can contain up to 24 items. |


<span id="periodicdate"></span>
### PeriodicDate


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Time |String |No |20:00~21:12 |Time period. You can specify multiple different time periods separated by commas (`,`), for example, `20:00~21:12,22:00~23:12`. 4 time periods can be configured at most. |
|Weekday |String |No |1,3,5 |Specific days within a week. You can specify multiple different time periods with commas (`,`). For example, `1,3,5` indicates Monday, Wednesday, and Friday of each week. 7 time periods can be configured at most. |
|DayOfMonth |String |No |2~3 |Specific days within a month. You can specify multiple different time periods separated by commas (`,`). For example, `2~3` indicates the 2nd and 3rd day of each month. 10 time periods can be configured at most. |


<span id="labelmatcher"></span>
### LabelMatcher


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Label |String |Yes |app |Label. |
|Value |String |Yes |test |Label Value. |
|Operator |String |No |Equal |The operator. Possible values:<br><br><br>* Equal: Equal<br><br>* NotEqual: Not equal<br><br>* RegexpEqual: Equal using a regular expression<br><br>* RegexpNotEqual: Not equal using a regular expression |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://vmp.cn-beijing.byteplusapi.com.cn?Action=CreateSilencePolicy&Version=2021-03-03
Content-Type: application/json
{
    "Name": "alert-silence-demo",
    "Description": "Description",
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
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |e28ae750\-bbb8\-4ff4\-abf4\*\*\* |Alert silence policy ID. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
HTTP/1.1: 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateSilencePolicy",
        "Version": "2021-03-03",
        "Service": "vmp",
        "Region": "cn-beijing"
    },
    "Result": {
        "Id": "e28ae750-bbb8-4ff4-abf4***"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The error codes for this API are listed in the table below. For a list of error codes for other APIs, see [Public error codes](https://docs.byteplus.com/en/docs/vmp/Common-error-codes).


|**HTTP status codes** |**Error code** |**Error messages** |**Descriptions** |
|---|---|---|---|
|400 |InvalidParameter.{{parameter}} |The specified parameter {{parameter}} is invalid. |An invalid parameter was found. For example, an invalid workspace name was included in requests. |
|400 |MissingParameter.{{parameter}} |The required parameter {{parameter}} is missing. |A required parameter is missing. |
|403 |ProductUnsubscribed |You are not subscribed to VMP. Please go to the VMP console web page to subscribe to the service |The current account is not subscribed to the VMP service. |
|409 |Conflict.Name |The specified name conflicts with existing {{resource}}. |The specified name has already been used by an existing resource. |

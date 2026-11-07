---
title: "ListAlertSamples"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/ListAlertSamples"
---

Obtain the historical records of alerts.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions

Vital Managed Service for Prometheus has been deployed in multiple regions worldwide, aiming to provide you with an experience of higher stability and lower latency. You can choose an access point that is optimal for the region of your services according to the [Service addresses](https://docs.byteplus.com/en/docs/vmp/Service_address) document.


* Request method: POST

* Request URL: https://vmp.cn\-beijing.byteplusapi.com.cn?Action=ListAlertSamples&Version=2021\-03\-03


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |ListAlertSamples |API name. The API name is `ListAlertSamples`. |
|Version |String |Yes |2021\-03\-03 |API version. The API version is `2021-03-03`. |
|Limit |Long |No |100 |Maximum records allowed to be returned. The default number is 100. You can set it to 500 at most. |
|Filter |Object of [AlertSampleFilter](https://docs.byteplus.com/en/docs/vmp/ListAlertSamples#alertsamplefilter) |Yes |\- |Filter conditions foralertecords. |


<span id="AlertSampleFilter"></span>
### AlertSampleFilter


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|AlertId |String |Yes |e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c |Filtered by IDs of alert records. |
|SampleSince |Long |No |1600885800 |The start of the time range to filter alert records. |
|SampleUntil |Long |No |1600885800 |The end of a time range for alert statistics. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vmp.cn-beijing.byteplusapi.com.cn/?Action=ListAlertSamples&Version=2021-03-03
Content-Type: application/json
{
    "Limit": 100,
    "Filter": {
        "AlertId": "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c",
        "SampleSince": 1600885800,
        "SampleUntil": 1600885800
    }
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Total |Long |100 |Total number of alert records. |
|Items |Array of [AlertSample](https://docs.byteplus.com/en/docs/vmp/ListAlertSamples#alertsample) |\- |A list of alert records. |


<span id="AlertSample"></span>
### AlertSample


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|AlertId |String |e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c |Alert record ID. |
|Timestamp |Long |1686232540 |The UNIX timestamp of the alert record. |
|Phase |String |Active |Statuses of alert records:<br><br><br>* **Pending**: it has reached or exceeded the threshold but has not lasted long enough yet<br><br>* **Active**: alert has been raised<br><br>* **Resolved**: cleared automatically<br><br>* **Disabled**: cleared by humans |
|Level |String |P0 |Levels of alert records. Level P0, P1, and P2 are available currently. |
|Value |Double |123.123 |The value obtained by using PromQL statement on alert rules. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1: 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListAlertSamples",
        "Version": "2021-03-03",
        "Service": "vmp",
        "Region": "cn-beijing"
    },
    "Result": {
        "Total": 100,
        "Items": [
            {
                "Level": "P0",
                "Phase": "Active",
                "Value": 123.123,
                "AlertId": "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c",
                "Timestamp": 1686232540
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The error codes for current API only are listed in the table below. See [Public error codes](https://docs.byteplus.com/en/docs/vmp/Common-error-codes) to view error codes for any APIs.


|HTTP status codes |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidParameter.{{parameter}} |The specified parameter {{parameter}} is invalid. |The specified parameter is invalid. |
|403 |ProductUnsubscribed |You are not subscribed to VMP. Please go to the VMP console web page to subscribe to the service |The account is not subscribed to the VMP Service. |

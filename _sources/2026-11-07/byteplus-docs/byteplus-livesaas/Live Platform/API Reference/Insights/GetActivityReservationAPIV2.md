---
title: "GetActivityReservationAPIV2"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/getactivityreservationapiv2"
---

Gets the booking information of a specific live room.

<span id="请求说明"></span>
## Requirements

Quota: 120 queries per minute per account

<span id="http-request"></span>
## HTTP request


* Method: GET

* Endpoint: https://livesaas.byteplusapi.com/?Action=GetActivityReservationAPIV2&Version=2020\-06\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Not all common request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`GetActivityReservationAPIV2` |API operation. |
|Version |String |Yes |`2020-06-01` |The version of this API operation. Current version: `2020-06-01`. |
|ActivityId |Long |Yes |`1779****58280` |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |
|Page |Integer |No |`1` |The number of the page to return. Default value: `1`. |
|PageSize |Integer |No |`10` |The number of results to return on each page. Default value: `10`. Value range: [1,500]. |
|Channel |String |No |`123` |Data from the channel with the specified channel identifier is to be returned. By default, data from all the channels is to be returned. You can get the channel identifier on the **Marketing toolkits** \> **Channels** page of the live room on the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/). |
|TelReserve |String |No |`182****5709` |The phone number used to book the live stream. |
|NickName |String |No |`Viewer A` |The nickname of the viewer who booked the live stream. Fuzzy search is supported. |
|ExternalId |String |No |`1234` |The unique identifier on third\-party platforms of the viewer. Fuzzy search is supported.<br><br>The ID varies based on how the viewer logs in to the live room. For more information, see [Viewer behavior data](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-data-statistics#viewer-behavior-data). You can use this ID to identify the viewer's identity within your organization, enabling user insights and data analysis as needed. |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|ActivityId |Long |`1779****58280` |The activity ID of the live room. |
|Total |Integer |`1` |The total number of returned results. |
|Page |Integer |`1` |The page number of the returned page. |
|Items |Array of [Items](https://docs.byteplus.com/en/docs/11/27531#items) |`-` |The list of viewers' booking information. |


<span id="items"></span>
### Items


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|NickName |String |`Viewer A` |The nickname of the viewer. |
|TelReserve |String |`182****5709` |The phone number used to book the live stream. |
|Ip |String |`192.***.***.1` |The IP address of the viewer. |
|IpAddress |String |`Beijing` |The region of the IP address. |
|SubmitTime |Integer |`1697080167` |The time when the viewer booked the live stream, in Unix timestamp format. Unit: seconds. |
|UserDevice |String |`Windows 10` |The device type used by the viewer to enter the live room. |
|ExternalId |String |`31210****54471` |The unique identifier on third\-party platforms of the viewer. You can use this ID to identify the viewer's identity within your organization, enabling user insights and data analysis as needed. |
|Extra |String |`abc` |Your extra parameter. |
|Channel |String |`123` |The channel identifier. |
|UserId |Long |`174466****363934` |The user ID, which is the unique identifier in BytePlus Live of the viewer. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
GET https://livesaas.byteplusapi.com/?Action=GetActivityReservationAPIV2&Version=2020-06-01&ActivityId=1779****58280&Page=1&PageSize=10&Channel=123&TelReserve=182****5709
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetActivityReservationAPIV2",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697080180
    },
    "Result": {
        "ActivityId": 1779****58280,
        "Total": 1,
        "Page": 1,
        "Items": [
            {
                "NickName": "Viewer A",
                "UserId": 174466****363934,
                "Channel": "123",
                "Extra": "abc",
                "ExternalId": "31210****54471",
                "UserDevice": "Windows 10",
                "SubmitTime": 1697080167,
                "IpAddress": "Beijing",
                "Ip": "192.*.*.1",
                "TelReserve": "182****5709"
            }
        ]
    }
}
```


<span id="error-codes"></span>
## Error codes

For a list of common error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).

&nbsp;

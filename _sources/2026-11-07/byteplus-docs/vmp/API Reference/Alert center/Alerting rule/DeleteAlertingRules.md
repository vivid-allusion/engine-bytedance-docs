---
title: "DeleteAlertingRules"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/DeleteAlertingRules"
---

Delete alerting rules.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions

Vital Managed Service for Prometheus has been deployed in multiple regions worldwide to provide you with a more stable, lower\-latency experience. You can choose an optimal access point for your service region by referring to the [Service addresses](https://docs.byteplus.com/en/docs/vmp/Service_address) topic.


* Request method: POST

* Request URL: https://vmp.cn\-beijing.byteplusapi.com.cn/?Action=DeleteAlertingRules&Version=2021\-03\-03


<span id="k1tYUXVq"></span>
## Debugging

[去调试]()


&nbsp;

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |DeleteAlertingRules |API name. The API name is `DeleteAlertingRules`. |
|Version |String |Yes |2021\-03\-03 |API version. The API version is `2021-03-03`. |
|Ids |Array of String |Yes |["e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c"] |Alerting rule ID. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vmp.cn-beijing.byteplusapi.com.cn/?Action=DeleteAlertingRules&Version=2021-03-03
Content-Type: application/json
{
    "Ids": [
        "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c"
    ]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|SuccessfulItems |Array of String |["e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c"] |A list of IDs for alerting rules that were deleted successfully. |
|UnsuccessfulItems |Array of [UnsuccessfulItem](https://docs.byteplus.com/en/docs/88/22106#unsuccessfulitem) |\- |Information about alerting rules that failed to be deleted. |


<span id="UnsuccessfulItem"></span>
### UnsuccessfulItem


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Id |String |e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c |ID of the object on which the action failed. |
|Error |Object of [UnsuccessfulItemError](https://docs.byteplus.com/en/docs/vmp/DeleteAlertingRules#unsuccessfulitemerror) |\- |Reason for failed actions. |


<span id="UnsuccessfulItemError"></span>
### UnsuccessfulItemError


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Code |String |NotFound.Ids |Error code. |
|Message |String |The specified Contact abc is not found. |Error message. |
|Data |JSON Map |\- |Error metadata. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1: 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DeleteAlertingRules",
        "Version": "2021-03-03",
        "Service": "vmp",
        "Region": "cn-beijing"
    },
    "Result": {
        "SuccessfulItems": [
            "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c"
        ],
        "UnsuccessfulItems": [
            {
                "Id": "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c",
                "Error": {
                    "Code": "NotFound.Ids",
                    "Message": "The specified Contact abc is not found."
                }
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
|400 |MissingParameter.{{parameter}} |The required parameter {{parameter}} is missing. |Missing required parameters. |
|403 |ProductUnsubscribed |You are not subscribed to VMP. Please go to the VMP console web page to subscribe to the service |The account is not subscribed to the VMP Service. |
|404 |NotFound.Id |The specified Contact/ContactGroup {{Id}} is not found. |The specified contact person/group was not found. |

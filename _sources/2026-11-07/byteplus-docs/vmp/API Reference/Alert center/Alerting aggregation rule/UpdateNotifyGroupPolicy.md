---
title: "UpdateNotifyGroupPolicy"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/UpdateNotifyGroupPolicy"
---

Update the alerting aggregation policy.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions

Vital Managed Service for Prometheus has been deployed in multiple regions worldwide, aiming to provide you with an experience of higher stability and lower latency. You can choose an access point that is the most optimal for the region of your services according to the [Service addresses](https://docs.byteplus.com/en/docs/vmp/Service_address) document.


* Request method: POST

* Request URL: https://vmp.cn\-beijing.byteplusapi.com.cn/?Action=UpdateNotifyGroupPolicy&Version=2021\-03\-03


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When Levels is provided, all three levels (P0, P1, and P2) must be included, and Level values must be unique.</div>



|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |UpdateNotifyGroupPolicy |API name. The API name is `UpdateNotifyGroupPolicy`. |
|Version |String |Yes |2021\-03\-03 |API version. The API version is `2021-03-03`. |
|Id |String |Yes |e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c |Alerting aggregation policy ID. |
|Name |String |No |test |Name of the alerting aggregation policy. |
|Description |String |No |This is a description |Description of the alerting aggregation policy. |
|Levels |Array of [NotifyGroupPolicyLevel](https://docs.byteplus.com/en/docs/vmp/UpdateNotifyGroupPolicy#notifygrouppolicylevel) |No |\- |Alerting aggregation policy level. |


<span id="NotifyGroupPolicyLevel"></span>
### NotifyGroupPolicyLevel


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Level |String |Yes |P0 |Aggregation policy level, including: P0, P1, P2. |
|GroupBy |Array of String |Yes |["__rule__"] |Aggregation dimension. Available value is **rule**. |
|GroupWait |String |No |30 |Waiting time. It is a positive integer in seconds. |
|GroupInterval |String |Yes |30 |Aggregation interval. It is a positive integer in seconds. |
|RepeatInterval |String |Yes |30 |Repeat interval. It is a positive integer in seconds. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vmp.cn-beijing.byteplusapi.com.cn/?Action=UpdateNotifyGroupPolicy&Version=2021-03-03
Content-Type: application/json
{
    "Id": "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c",
    "Name": "test",
    "Description": "This is a description",
    "Levels": [
        {
            "Level": "P0",
            "GroupBy": [
                "This"
            ],
            "GroupWait": "30",
            "GroupInterval": "30",
            "RepeatInterval": "30"
        }
    ]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Id |String |e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c |Alerting aggregation policy ID. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1: 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdateNotifyGroupPolicy",
        "Version": "2021-03-03",
        "Service": "vmp",
        "Region": "cn-beijing"
    },
    "Result": {
        "Id": "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The error codes for current API only are listed in the table below. See [Public error codes](https://docs.byteplus.com/en/docs/vmp/Common-error-codes) to view error codes for any APIs.


|HTTP status codes |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidParameter.{{parameter}} |The specified parameter {{parameter}} is invalid. |The specified parameter is invalid. |
|400 |MissingParameter.{{parameter}} |The required parameter {{parameter}} is missing. |Missing required parameters. |
|403 |ProductUnsubscribed |You are not subscribed to VMP. Please go to the VMP console web page to subscribe to the service |The account is not subscribed to the VMP Service. |
|404 |NotFound.Id |The specified Contact/ContactGroup {{Id}} is not found. |The specified contact person/group was not found. |
|409 |Conflict.Name |The specified name conflicts with existing {{resource}}. |The specified name has already been used by an existing resource. |

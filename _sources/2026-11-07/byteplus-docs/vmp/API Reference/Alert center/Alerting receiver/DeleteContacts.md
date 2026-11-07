---
title: "DeleteContacts"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/DeleteContacts"
---

Delete alert contacts.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions

Vital Managed Service for Prometheus has been deployed in multiple regions worldwide, aiming to provide you with an experience of higher stability and lower latency. You can choose an optimal access point for your service region by referring to the [Service addresses](https://docs.byteplus.com/en/docs/vmp/Service_address) topic.


* Request method: POST

* Request URL: https://vmp.cn\-beijing.byteplusapi.com.cn/?Action=DeleteContacts&Version=2021\-03\-03


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |DeleteContacts |API name. The API name is `DeleteContacts`. |
|Version |String |Yes |2021\-03\-03 |API version. The API version is `2021-03-03`. |
|Ids |Array of String |Yes |["e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c"] |Contact person ID. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vmp.cn-beijing.byteplusapi.com.cn/?Action=DeleteContacts&Version=2021-03-03
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
|SuccessfulItems |Array of String |["e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c"] |The contact person IDs that were deleted successfully. |
|UnsuccessfulItems |Array of [UnsuccessfulItem](https://docs.byteplus.com/en/docs/vmp/DeleteContacts#unsuccessfulitem) |\- |Information of the contact persons that failed to be deleted. |


<span id="UnsuccessfulItem"></span>
### UnsuccessfulItem


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Id |String |e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c |IDs of objects on which actions failed. |
|Error |Object of [UnsuccessfulItemError](https://docs.byteplus.com/en/docs/vmp/DeleteContacts#unsuccessfulitemerror) |\- |Reason for failed actions. |


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
        "Action": "DeleteContacts",
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

The following table lists the error codes specific to this API. For public error codes, See [Public error codes](https://docs.byteplus.com/en/docs/vmp/Common-error-codes).


|HTTP status codes |Error codes |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.{{parameter}} |The required parameter {{parameter}} is missing. |Missing required parameters. |
|403 |ProductUnsubscribed |You are not subscribed to VMP. Please go to the VMP console web page to subscribe to the service |The account is not subscribed to the VMP Service. |
|404 |NotFound.Id |The specified Contact/ContactGroup {{Id}} is not found. |The specified contact person/group was not found. |

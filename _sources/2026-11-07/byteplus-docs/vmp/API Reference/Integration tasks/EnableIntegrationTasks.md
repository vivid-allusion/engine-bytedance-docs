---
title: "EnableIntegrationTasks"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/EnableIntegrationTasks"
---

Enable integration tasks.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

VMP has been deployed in multiple regions worldwide, aiming to provide you with an experience of higher stability and lower latency. You can choose an access point that is optimal for the region of your services according to the [Service addresses](https://docs.byteplus.com/en/docs/vmp/Service_address) document.


* Request method: POST

* Request URL: https://vmp.cn\-beijing.byteplusapi.com.cn/?Action=EnableIntegrationTasks&Version=2021\-03\-03


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |EnableIntegrationTasks |The name of the API. The name of this API is `EnableIntegrationTasks`. |
|Version |String |Yes |2021\-03\-03 |API version. The API version is `2021-03-03`. |
|Ids |Array of String |Yes |["fcbc7eef\-2f6c\-4247\-bce1\*\*\*"] |IDs of integration tasks. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://vmp.cn-beijing.byteplusapi.com.cn/?Action=EnableIntegrationTasks&Version=2021-03-03
Content-Type: application/json
{
    "Ids": [
        "fcbc7eef-2f6c-4247-bce1***"
    ]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|SuccessfulItems |Array of String |["fcbc7eef\-2f6c\-4247\-bce1\*\*\*"] |IDs of successfully enabled integration tasks. |
|UnsuccessfulItems |Array of [UnsuccessfulItem](https://docs.byteplus.com/en/docs/88/69227#unsuccessfulitem) |\- |IDs of integration task that failed to be enabled. |


<span id="unsuccessfulitem"></span>
### UnsuccessfulItem


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |e28ae750\-bbb8\-4ff4\-abf4\*\*\* |IDs of objects on which actions failed. |
|Error |Object of [UnsuccessfulItemError](https://docs.byteplus.com/en/docs/88/69227#unsuccessfulitemerror) |\- |Reason for failed actions. |


<span id="unsuccessfulitemerror"></span>
### UnsuccessfulItemError


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Code |String |NotFound.Ids |Error code. For details, see [Error codes](https://docs.byteplus.com/en/docs/88/69227#.6ZSZ6K-v56CB) or [Public error codes](https://docs.byteplus.com/en/docs/vmp/Common-error-codes). |
|Message |String |The specified Contact abc was not found. |Error message. For details, see [Error codes](https://docs.byteplus.com/en/docs/88/69227#.6ZSZ6K-v56CB) or [Public error codes](https://docs.byteplus.com/en/docs/vmp/Common-error-codes). |
|Data |JSON Map |\- |Error metadata. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
HTTP/1.1: 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "EnableIntegrationTasks",
        "Version": "2021-03-03",
        "Service": "vmp",
        "Region": "cn-beijing"
    },
    "Result": {
        "SuccessfulItems": [
            "fcbc7eef-2f6c-4247-bce1***"
        ],
        "UnsuccessfulItems": [
            {
                "Id": "e28ae750-bbb8-4ff4-abf4***",
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

The error codes for this API are listed in the table below. For a list of error codes for other APIs, see [Public error codes](https://docs.byteplus.com/en/docs/vmp/Common-error-codes).


|**HTTP status code** |**Error code** |**Error message** |**Description** |
|---|---|---|---|
|403 |ProductUnsubscribed |You are not subscribed to VMP. Please go to the VMP console web page to subscribe to the service |The account is not subscribed to the VMP service. |
|404 |NotFound.Id |The specified Contact/ContactGroup {{Id}} is not found. |The specified contact person/group was not found. |
|400 |MissingParameter.{{parameter}} |The required parameter {{parameter}} is missing. |A required parameter is missing. |

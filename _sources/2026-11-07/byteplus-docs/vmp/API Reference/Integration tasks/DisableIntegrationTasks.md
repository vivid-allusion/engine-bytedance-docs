---
title: "DisableIntegrationTasks"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/DisableIntegrationTasks"
---

Disable integration tasks.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

Vital Managed Service for Prometheus has been deployed in multiple regions worldwide, aiming to provide you with an experience of higher stability and lower latency. You can choose an access point that is the most optimal for the region of your services according to the [Service addresses](https://docs.byteplus.com/en/docs/vmp/Service_address) document.


* Request method: POST

* Request URL: https://vmp.cn\-beijing.byteplusapi.com.cn/?Action=DisableIntegrationTasks&Version=2021\-03\-03


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required or not** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |DisableIntegrationTasks |API name. The name of this API is `DisableIntegrationTasks`. |
|Version |String |Yes |2021\-03\-03 |API version. The API version is `2021-03-03`. |
|Ids |Array of String |Yes |["fcbc7eef\-2f6c\-4247\-bce1\*\*\*"] |IDs of integration tasks. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://vmp.cn-beijing.byteplusapi.com.cn/?Action=DisableIntegrationTasks&Version=2021-03-03
Content-Type: application/json
{
    "Ids": [
        "fcbc7eef-2f6c-4247-bce1***"
    ]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|SuccessfulItems |Array of String |["fcbc7eef\-2f6c\-4247\-bce1\*\*\*"] |IDs of successfully disabled integration tasks. |
|UnsuccessfulItems |Array of [UnsuccessfulItem](https://docs.byteplus.com/en/docs/88/69222#unsuccessfulitem) | |IDs of integration tasks that failed to be disabled. |


<span id="unsuccessfulitem"></span>
### UnsuccessfulItem


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |e28ae750\-bbb8\-4ff4\-abf4\*\*\* |IDs of objects on which actions failed. |
|Error |Object of [UnsuccessfulItemError](https://docs.byteplus.com/en/docs/88/69222#unsuccessfulitemerror) |\- |Reason for failed actions. |


<span id="unsuccessfulitemerror"></span>
### UnsuccessfulItemError


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Code |String |NotFound.Ids |Error code. For details, See [Error codes](https://docs.byteplus.com/en/docs/88/69222#.6ZSZ6K-v56CB) or [Public error codes](https://docs.byteplus.com/en/docs/vmp/Common-error-codes). |
|Message |String |The specified Contact abc is not found. |Error message. For details, See [Error codes](https://docs.byteplus.com/en/docs/88/69222#.6ZSZ6K-v56CB) or [Public error codes](https://docs.byteplus.com/en/docs/vmp/Common-error-codes). |
|Data |JSON Map |\- |Error metadata. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
HTTP/1.1: 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DisableIntegrationTasks",
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

The error codes for current API only are listed in the table below. See [Public error](https://docs.byteplus.com/en/docs/vmp/Common-error-codes) codes to view error codes for any APIs.


|**HTTP status code** |**Error code** |**Error message** |**Description** |
|---|---|---|---|
|403 |ProductUnsubscribed |You are not subscribed to VMP. Please go to the VMP console web page to subscribe to the service |The account is not subscribed to VMP Service. |
|404 |NotFound.Id |The specified Contact/ContactGroup {{Id}} is not found. |The specified contact person/group was not found. |
|400 |MissingParameter.{{parameter}} |The required parameter {{parameter}} is missing. |Missing necessary parameters. |

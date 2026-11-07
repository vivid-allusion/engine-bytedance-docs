---
title: "TestWebhook"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/TestWebhook"
---

Test the connectivity of the Webhook.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

Vital Managed Service for Prometheus has been deployed in multiple regions worldwide, aiming to provide you with an experience of higher stability and lower latency. You can choose an access point that is the most optimal for the region of your services according to the [Service addresses](https://docs.byteplus.com/en/docs/vmp/Service_address) document.


* Request method: POST

* Request URL: https://vmp.cn\-beijing.byteplusapi.com.cn/?Action=TestWebhook&Version=2021\-03\-03


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |TestWebhook |API name. The API name is `TestWebhook`. |
|Version |String |Yes |2021\-03\-03 |API version. The API version is `2021-03-03`. |
|Address |String |Yes |https://bytedance.com/v2/hook/f19ce\*\*\* |Webhook address. |
|Token |String |No |zs0T\*\*\*\* |Webhook token. It cannot be configured alone. When you configure a Webhook address and enable signature verification, you must also configure this token. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vmp.cn-beijing.byteplusapi.com.cn/?Action=TestWebhook&Version=2021-03-03
Content-Type: application/json
{
    "Address": "https://bytedance.com/v2/hook/f19ce***",
    "Token": "zs0T****"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|StatusCode |Integer |200 |HTTP status code. |
|Body |String |successfully |HTTP response body. |
|ErrorMessage |String |timeout |Error messages in response to HTTP requests. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1: 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "TestWebhook",
        "Version": "2021-03-03",
        "Service": "vmp",
        "Region": "cn-beijing"
    },
    "Result": {
        "StatusCode": 200,
        "Body": "successfully",
        "ErrorMessage": "timeout"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The error codes for current API only are listed in the table below. See [Public error codes](https://docs.byteplus.com/en/docs/vmp/Common-error-codes) to view error codes for any APIs.


|HTTP status codes |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidParameter.{{parameter}} |The specified parameter {{parameter}} is invalid. |The specified parameter is invalid. |
|400 |MissingParameter.{{parameter}} |The required parameter {{parameter}} is missing. |Missing required parameters. |
|403 |ProductUnsubscribed |You are not subscribed to VMP. Please go to the VMP console web page to subscribe to the service |The account is not subscribed to the VMP Service. |

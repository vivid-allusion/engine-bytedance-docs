---
title: "TestLarkBotWebhook"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/TestLarkBotWebhook"
---

Test the connectivity of the Feishu group bot.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions

Vital Managed Service for Prometheus has been deployed in multiple regions worldwide, aiming to provide you with an experience of higher stability and lower latency. You can choose an access point that is the most optimal for the region of your services according to the [Service addresses](https://docs.byteplus.com/en/docs/vmp/Service_address) document.


* Request method: POST

* Request URL: https://vmp.cn\-beijing.byteplusapi.com.cn/?Action=TestLarkBotWebhook&Version=2021\-03\-03


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Types |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |TestLarkBotWebhook |API name. The API name is `TestLarkBotWebhook`. |
|Version |String |Yes |2021\-03\-03 |API version. The API version is `2021-03-03`. |
|Address |String |Yes |https://open.feishu.cn/open\-apis/bot/v2/hook/f19\*\*\* |The Webhook address of the Feishu group bot. See [Lark Documentation](https://open.feishu.cn/document/client-docs/bot-v3/bot-overview). |
|SecretKey |String |No |zs0T\*\*\* |The Webhook secret key of the Feishu group bot. It cannot exist alone. When you configure a Feishu group bot Webhook address and enable signature verification, you must also configure this secret key. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vmp.cn-beijing.byteplusapi.com.cn/?Action=TestLarkBotWebhook&Version=2021-03-03
Content-Type: application/json
{
    "Address": "https://open.feishu.cn/open-apis/bot/v2/hook/f19***",
    "SecretKey": "zs0T***"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|StatusCode |Integer |200 |HTTP status code. |
|ErrorMessage |String |timeout |Error messages in response to HTTP requests. |
|LarkCode |Integer |0 |The status code returned after the Feishu bot sends a message. |
|LarkMessage |String |ok |The message returned after the Feishu bot sends a message. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1: 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "TestLarkBotWebhook",
        "Version": "2021-03-03",
        "Service": "vmp",
        "Region": "cn-beijing"
    },
    "Result": {
        "StatusCode": 200,
        "ErrorMessage": "timeout",
        "LarkCode": 0,
        "LarkMessage": "ok"
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

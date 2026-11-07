---
title: "TestDingTalkBotWebhook"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/TestDingTalkBotWebhook"
---

Test the connectivity of the DingTalk group bot.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions

Vital Managed Service for Prometheus has been deployed in multiple regions worldwide, aiming to provide you with an experience of higher stability and lower latency. You can choose an access point that is the most optimal for the region of your services according to the [Service addresses](https://docs.byteplus.com/en/docs/vmp/Service_address) document.


* Request method: POST

* Request URL: https://vmp.cn\-beijing.byteplusapi.com.cn/?Action=TestDingTalkBotWebhook&Version=2021\-03\-03


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |TestDingTalkBotWebhook |API name. The API name is `TestDingTalkBotWebhook`. |
|Version |String |Yes |2021\-03\-03 |API version. The API version is `2021-03-03`. |
|Address |String |Yes |https://oapi.dingtalk.com/robot/send?access_token=\*\*\* |The Webhook address of the DingTalk group bot. See the [DingTalk User Guide](https://open.dingtalk.com/document/robots/custom-robot-access) for details. |
|SecretKey |String |No |zs0T\*\*\* |The Webhook secret key of the DingTalk group bot. It cannot be configured alone. The Webhook secret key of the DingTalk group bot. It cannot be configured alone. |
|AtMobiles |Array of String |No |["133\*\*\*\*\*\*\*\*"] |The phone number of the user @mentioned. |
|AtUserIds |Array of String |No |["\*\*\*\*\*\*\*\*"] |The ID of the user @mentioned. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vmp.cn-beijing.byteplusapi.com.cn/?Action=TestDingTalkBotWebhook&Version=2021-03-03
Content-Type: application/json
{
    "Address": "https://oapi.dingtalk.com/robot/send?access_token=***",
    "SecretKey": "zs0T***",
    "AtMobiles": [
        "133********"
    ],
    "AtUserIds": [
        "********"
    ]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|StatusCode |Integer |200 |HTTP status code. |
|ErrorMessage |String |timeout |Error messages in response to HTTP requests. |
|DingTalkCode |Integer |9499 |The status code returned after DingTalkBot sends a message. |
|DingTalkMessage |String |Bad Request |The message returned after the DingTalk bot sends a message. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1: 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "TestDingTalkBotWebhook",
        "Version": "2021-03-03",
        "Service": "vmp",
        "Region": "cn-beijing"
    },
    "Result": {
        "StatusCode": 200,
        "ErrorMessage": "timeout",
        "DingTalkCode": 9499,
        "DingTalkMessage": "Bad Request"
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

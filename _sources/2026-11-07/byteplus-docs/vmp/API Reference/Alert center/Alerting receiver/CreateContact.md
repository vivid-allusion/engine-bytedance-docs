---
title: "CreateContact"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/CreateContact"
---

Create an alerting contact.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions

Vital Managed Service for Prometheus has been deployed in multiple regions worldwide, aiming to provide you with an experience of higher stability and lower latency. You can choose an optimal access point for your service region by referring to the [Service addresses](https://docs.byteplus.com/en/docs/vmp/Service_address) topic.


* Request method: POST

* Request URL: https://vmp.cn\-beijing.byteplusapi.com.cn/?Action=CreateContact&Version=2021\-03\-03


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateContact&serviceCode=vmp&version=2021-03-03&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |CreateContact |The name of the API. The API name is `CreateContact`. |
|Version |String |Yes |2021\-03\-03 |The API version. The API version is `2021-03-03`. |
|Name |String |Yes |user\-demo |The name of the contact.<br><br><br>* It can only contain uppercase and lowercase letters, Chinese characters, digits, hyphens (\-), and underscores (_).<br><br>* The name cannot start with a digit, a hyphen (\-), an underscore (_), or other special characters.<br><br>* It must be fewer than 128 characters in length.<br><br>* It needs to be unique under the same account. |
|Email |String |No |user\-demo@example.com |The email address of the contact, which needs to be a valid email address. |
|Webhook |Object of [Webhook](https://docs.byteplus.com/en/docs/88/22092#webhook) |No |\- |The generic webhook of the contact. |
|ContactGroupIds |Array of String |No |["e28ae750\-bbb8\-4ff4\-abf4\*\*\*"] |The ID of the contact group to which the contact belongs. |
|LarkBotWebhook |Object of [LarkBotWebhook](https://docs.byteplus.com/en/docs/88/22092#larkbotwebhook) |No |\- |The webhook of Larkbot. |
|DingTalkBotWebhook |Object of [DingTalkBotWebhook](https://docs.byteplus.com/en/docs/88/22092#dingtalkbotwebhook) |No |\- |The webhook of the DingTalk robot. |
|WeComBotWebhook |Object of [WeComBotWebhook](https://docs.byteplus.com/en/docs/88/22092#wecombotwebhook) |No |\- |The webhook of the WeCom robot. |


<span id="webhook"></span>
### Webhook


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Address |String |Yes |https://www.bytedance.com/ |The generic webhook address. |
|Token |String |No |3KSxxx |The token for the generic webhook. It needs to be used together with the generic webhook address. |


<span id="larkbotwebhook"></span>
### LarkBotWebhook


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Address |String |Yes |https://open.feishu.cn/open\-apis/bot/v2/hook/\*\*\* |The webhook address of Larkbot. See [User guide](https://open.feishu.cn/document/client-docs/bot-v3/bot-overview) for details. |
|SecretKey |String |No |6KKxxx |The webhook secret key of Larkbot. It needs to be used together with the webhook address of Larkbot. |


<span id="dingtalkbotwebhook"></span>
### DingTalkBotWebhook


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Address |String |Yes |https://oapi.dingtalk.com/robot/send?access_token=\*\*\* |The webhoot address of the DingTalk bot. See [User Guide](https://open.dingtalk.com/document/robots/custom-robot-access) for details. |
|SecretKey |String |No |SECxxx |The webhook secret key of the DingTalk robot. It needs to be used together with the webhook address of the DingTalk robot. |
|AtMobiles |Array of String |No |["133\*\*\*\*\*\*\*\*"] |The phone number of the user who is about to be @mentioned in the group. |
|AtUserIds |Array of String |No |["\*\*\*\*\*\*\*\*"] |The ID of the user who is about to be @mentioned in the group. |


<span id="wecombotwebhook"></span>
### WeComBotWebhook


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Address |String |Yes |https://qyapi.weixin.qq.com/cgi\-bin/webhook/send?key=\*\*\* |The webhook address of the WeCom robot. See [User guide](https://developer.work.weixin.qq.com/document/path/91770) for details. |
|AtUserIds |Array of String |No |["\*\*\*\*\*\*\*\*"] |The ID of the user who is about to be @mentioned in the group. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vmp.cn-beijing.byteplusapi.com.cn/?Action=CreateContact&Version=2021-03-03
Content-Type: application/json
{
    "Name": "user-demo",
    "Email": "user-demo@example.com",
    "Webhook": {
        "Token": "3KSxxx",
        "Address": "https://www.bytedance.com/"
    },
    "ContactGroupIds": [
        "e28ae750-bbb8-4ff4-abf4***"
    ],
    "LarkBotWebhook": {
        "Address": "https://open.feishu.cn/open-apis/bot/v2/hook/***",
        "SecretKey": "6KKxxx"
    },
    "DingTalkBotWebhook": {
        "Address": "https://oapi.dingtalk.com/robot/send?access_token=***",
        "AtMobiles": [
            "133********"
        ],
        "AtUserIds": [
            "********"
        ],
        "SecretKey": "SECxxx"
    },
    "WeComBotWebhook": {
        "Address": "https://qyapi.weixin.qq.com/cgi-bin/webhook/send?key=xxxxxxx",
        "AtUserIds": [
            "********"
        ]
    }
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |e28ae750\-bbb8\-4ff4\-abf4\*\*\* |The contact ID. |
|SendStatus |String |MessageSucceed.Email |The status code returned when verification emails were being sent. Valid values:<br><br><br>* **AlreadyActive.Email**: The email address has already been activated.<br><br>* **MessageFailed.Email**: The verification email failed to be sent.<br><br>* **LimitExceeded.Email**: The email is sent too frequently.<br><br>* **MessageSucceed.Email**: The verification email has been sent. |
|Message |String |The same email address should not be validated more than once in 1 minute, please try it later. |The reason for the error occurred when verification emails were being sent.<br><br>This parameter has a value if the value of the `SendStatus` parameter is not `MessageSucceed.Email`. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1: 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateContact",
        "Version": "2021-03-03",
        "Service": "vmp",
        "Region": "cn-beijing"
    },
    "Result": {
        "Id": "e28ae750-bbb8-4ff4-abf4***",
        "SendStatus": "MessageSucceed.Email",
        "Message": "The same email address should not be validated more than once in 1 minute, please try it later."
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes of the API. For public error codes, see [Public error codes](https://docs.byteplus.com/en/docs/vmp/Common-error-codes).


|**HTTP status code** |**Error code** |**Error message** |**Description** |
|---|---|---|---|
|400 |InvalidParameter.{{parameter}} |The specified parameter {{parameter}} is invalid. |An invalid parameter was found. For example, an invalid workspace name was included in requests. |
|400 |MissingParameter.{{parameter}} |The required parameter {{parameter}} is missing. |A required parameter is missing. |
|403 |ProductUnsubscribed |You are not subscribed to VMP. Please go to the VMP console web page to subscribe to the service. |The account has not subscribed to the VMP service. |
|409 |Conflict.Name |The specified name conflicts with existing {{resource}}. |The specified name has already been used by an existing resource. |

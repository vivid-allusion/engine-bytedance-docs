---
title: "UpdateContact"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/UpdateContact"
---

Update alerting contacts.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions

Vital Managed Service for Prometheus has been deployed in multiple regions worldwide, aiming to provide you with an experience of higher stability and lower latency. You can choose an access point that is the most optimal for the region of your services according to the [Service addresses](https://docs.byteplus.com/en/docs/vmp/Service_address) document.


* Request method: POST

* Request URL: https://vmp.cn\-beijing.byteplusapi.com.cn/?Action=UpdateContact&Version=2021\-03\-03


<span id="JkQYkboj"></span>
## Debugging

[去调试]()


&nbsp;

<span id="Nw2iMAa0"></span>
## Request parameters


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |UpdateContact |API name. The API name is `UpdateContact`. |
|Version |String |Yes |2021\-03\-03 |API version. The API version is `2021-03-03`. |
|Id |String |Yes |e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c |ID of the contact person. |
|Name |String |No |user\-demo |Name of the contact person.<br><br><br>* It can only contain uppercase and lowercase letters, Chinese characters, numbers, hyphens, and underscores.<br><br>* It cannot start with numbers, hyphens, underscores (_), or other special characters.<br><br>* It must be less than 128 characters in length.<br><br>* It needs to be unique under the same account. |
|Email |String |No |user\-demo@example.com |A valid email address of the contact person. |
|Webhook |Object of [Webhook](https://docs.byteplus.com/en/docs/vmp/UpdateContact#webhook) |No |\- |Generic webhook for contacts. |
|ContactGroupIds |Array of String |No |["e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c"] |The contact group ID to which the contact person belongs. |
|LarkBotWebhook |Object of [LarkBotWebhook](https://docs.byteplus.com/en/docs/vmp/UpdateContact#larkbotwebhook) |No |\- |Webhook configuration of the Feishu group bot for the contact. |
|DingTalkBotWebhook |Object of [DingTalkBotWebhook](https://docs.byteplus.com/en/docs/vmp/UpdateContact#dingtalkbotwebhook) |No |\- |Webhook configuration of the DingTalk group bot for the contact. |
|WeComBotWebhook |Object of [WeComBotWebhook](https://docs.byteplus.com/en/docs/vmp/UpdateContact#wecombotwebhook) |No |\- |Webhook configuration of the WeCom group bot for the contact. |


<span id="Webhook"></span>
### Webhook


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Address |String |Yes |https://www.bytedance.com/ |Generic webhook address. |
|Token |String |No |3KSxxx |Authentication token for the generic webhook. It must be used together with the generic webhook address. |


<span id="LarkBotWebhook"></span>
### LarkBotWebhook


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Address |String |Yes |https://open.feishu.cn/open\-apis/bot/v2/hook/\*\*\* |The webhook address of the Feishu group bot. See [User Guide](https://open.feishu.cn/document/client-docs/bot-v3/bot-overview) for details. |
|SecretKey |String |No |6KKxxx |A webhook secret key for the Feishu group bot. It needs to always be used together with the webhook address of the Feishu group bot. |


<span id="DingTalkBotWebhook"></span>
### DingTalkBotWebhook


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Address |String |Yes |https://oapi.dingtalk.com/robot/send?access_token=\*\*\* |The webhook address of the DingTalk group bot. See [User Guide](https://open.dingtalk.com/document/robots/custom-robot-access) for details. |
|SecretKey |String |No |SECxxx |A webhook secret key for DingTalk robot. It needs to always be used together with the webhook address of DingTalk robot. |
|AtMobiles |Array of String |No |["133\*\*\*\*\*\*\*\*"] |The phone number of the user to be @mentioned. The user must be in the group. |
|AtUserIds |Array of String |No |["\*\*\*\*\*\*\*\*"] |The ID of the user who is about to be @mentioned in the group. |


<span id="WeComBotWebhook"></span>
### WeComBotWebhook


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Address |String |Yes |https://qyapi.weixin.qq.com/cgi\-bin/webhook/send?key=\*\*\* |The Webhook address of WeCom robot. See [User Guide](https://developer.work.weixin.qq.com/document/path/91770) for details. |
|AtUserIds |Array of String |No |["\*\*\*\*\*\*\*\*"] |The ID of the user who is about to be @mentioned in the group. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vmp.cn-beijing.byteplusapi.com.cn/?Action=CreateContact&Version=2021-03-03
Content-Type: application/json
{
    "Id": "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c",
    "Name": "user-demo",
    "Email": "user-demo@example.com",
    "Webhook": {
        "Token": "3KSxxx",
        "Address": "https://www.bytedance.com/"
    },
    "ContactGroupIds": [
        "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c"
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
        "Address": "https://qyapi.weixin.qq.com/cgi-bin/webhook/send?key=***",
        "AtUserIds": [
            "********"
        ]
    }
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Id |String |e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c |ID of the contact person. |
|SendStatus |String |MessageSucceed.Email |The status returned when sending verification emails:<br><br><br>* **AlreadyActive.Email**: the email address has already been verified<br><br>* **MessageFailed.Email**: failed to send the verification email<br><br>* **LimitExceeded.Email**: email sending is too frequent<br><br>* **MessageSucceed.Email**: verification email has been sent successfully |
|Message |String |The same email address should not be validated more than once in 1 minute, please try it later. |The reason the error occurred when sending the verification email. This parameter has a value when `SendStatus` is not `MessageSucceed.Email`. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1: 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdateContact",
        "Version": "2021-03-03",
        "Service": "vmp",
        "Region": "cn-beijing"
    },
    "Result": {
        "Id": "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c",
        "SendStatus": "MessageSucceed.Email",
        "Message": "The same email address should not be validated more than once in 1 minute, please try it later."
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The error codes for current API only are listed in the table below. See [Public error codes](https://docs.byteplus.com/en/docs/vmp/Common-error-codes) to view error codes for any APIs.


|HTTP status codes |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidParameter.{{parameter}} |The specified parameter {{parameter}} is invalid. |The input is invalid. For example, the workspace name does not meet the requirements. |
|400 |MissingParameter.{{parameter}} |The required parameter {{parameter}} is missing. |Missing required parameters. |
|403 |ProductUnsubscribed |You are not subscribed to VMP. Please go to the VMP console web page to subscribe to the service |The account is not subscribed to the VMP Service. |
|404 |NotFound.Id |The specified Contact/ContactGroup {{Id}} is not found. |The specified contact person/group was not found. |
|409 |Conflict.Name |The specified name conflicts with existing {{resource}}. |The specified name has already been used by an existing resource. |

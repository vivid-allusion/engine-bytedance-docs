---
title: "CreateNotification"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/CreateNotification"
---

Create a notification policy.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions


* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=CreateNotification&Version=2018\-01\-01


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateNotification&serviceCode=Volc_Observe&version=2018-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |CreateNotification |The name of the API. The API name is `CreateNotification`. |
|Version |String |Yes |2018\-01\-01 |The API version. The current API version is `2018-01-01`. |
|Name |String |No |notification\-demo |Notification policy name.<br><br><br>* The value range is 1 to 128.<br><br>* It cannot start with a digit or hyphen. |
|Notifications |Array of [Notify](https://docs.byteplus.com/en/docs/39/45541#notify) |No |\- |Notification policy details. |
|EffectStartAt |String |No |00:00 |The time when the notification policy starts taking effect. The time is in the format `HH:MM` (example: 00:00). |
|EffectEndAt |String |No |23:59 |The time when the notification policy stops being in effect. The time is in the format `HH:MM` (example: 23:59).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The <code>EffectEndAt</code> time must be later than the <code>EffectStartAt</code> time.</div><br> |


<span id="notify"></span>
### Notify


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Level |String |No |notice |Alert notification level. Valid values:<br><br><br>* **notice**<br><br>* **warning**<br><br>* **critical**<br><br>* **recovery** |
|WebhookIds |Array of String |No |18913208\*\*\*4528 |Webhook callback ID.<br><br>You can call the [ListWebhooks](https://docs.byteplus.com/en/docs/cloudmonitor/ListWebhooks) API to obtain Webhook callback IDs. |
|AlertMethods |Array of String |No |Email |Alert notification method. Values:<br><br><br>* **Email**: Receive alert notifications by email.<br><br>* **Phone**: Receive alert notifications by phone call.<br><br>* **SMS**: Receive alert notifications by Short Message Service (SMS).<br><br>* **Webhook**: Receive alert notifications by Webhook. |
|ContactGroupIds |Array of String |No |145080093687100\*\*\*\* |Alert contact group ID.<br><br>You can call the [ListContactGroups](https://docs.byteplus.com/en/docs/cloudmonitor/ListContactGroups) API to query contact group IDs. |
|NotifyTemplates |Array of [NotifyTemplateBasic](https://docs.byteplus.com/en/docs/39/45541#notifytemplatebasic) |No |\- |Notification template configuration. |


<span id="notifytemplatebasic"></span>
### NotifyTemplateBasic


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Channel |String |No |email |Notification channel. Values:<br><br><br>* **email**: Email<br><br>* **sms**: SMS<br><br>* **phone**: Phone call<br><br>* **lark**: Feishu<br><br>* **dingtalk**: DingTalk<br><br>* **wecom**: WeCom<br><br>* **slack**: Slack<br><br>* **api**: Callback address |
|NotifyTemplateId |String |No |189828\*\*\*00 |Notification template ID.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Only one notification template ID can be specified for each notification channel.</div><br> |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=CreateNotification&Version=2018-01-01
Content-Type: application/json
{
    "Name": "notification-demo",
    "Notifications": [
        {
            "Level": "notice",
            "WebhookIds": [
                "18913208***4528"
            ],
            "AlertMethods": [
                "Email"
            ],
            "ContactGroupIds": [
                "145080093687100****"
            ],
            "NotifyTemplates": [
                {
                    "Channel": "email",
                    "NotifyTemplateId": "189828***00"
                }
            ]
        }
    ],
    "EffectStartAt": "00:00",
    "EffectEndAt": "23:59"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Data |Array of String |189898\*\*\*00 |Notification policy ID. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "CreateNotification",
        "Region": "cn-beijing",
        "Service": "cloudmonitor",
        "Version": "2018-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Data": [
            "189898***00"
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no error codes specific to this API. For more information, see [Error codes](https://docs.byteplus.com/en/docs/cloudmonitor/Common-error-codes).

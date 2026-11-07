---
title: "EnablePresetAlertTemplate"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/EnablePresetAlertTemplate"
---

Enable a preset alert template to create alert policies in batches.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions


* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=EnablePresetAlertTemplate&Version=2018\-01\-01


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=EnablePresetAlertTemplate&serviceCode=Volc_Observe&version=2018-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |EnablePresetAlertTemplate |The name of the API. The API name is `EnablePresetAlertTemplate`. |
|Version |String |Yes |2018\-01\-01 |The API version. The current API version is `2018-01-01`. |
|TemplateId |String |Yes |1354766247190\*\*\*\*\*\* |Alert template ID. |
|NotificationId |String |No |189898\*\*\*00 |Notification policy ID.<br><br>You can call the [ListNotifications](https://docs.byteplus.com/en/docs/cloudmonitor/ListNotifications) API to query notification policy IDs.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This parameter has higher priority than <code>AlertMethods</code>. Therefore, when you use this parameter to specify alert notification policy IDs, other alert notification configurations (including <code>AlertMethods</code>, <code>ContactGroupIds</code>, <code>WebhookIds</code>, <code>EffectStartAt</code>, and <code>EffectEndAt</code>) will become invalid.</div><br> |
|AlertMethods |Array of String |No |Phone |Alert notification method. Values:<br><br><br>* **Email**: Receive alert notifications by email.<br><br>* **Phone**: Receive alert notifications by phone.<br><br>* **SMS**: Receive alert notifications by Short Message Service (SMS).<br><br>* **Webhook**: Receive alert notifications by Webhook. |
|ContactGroupIds |Array of String |No |["145080093687100\*\*\*\*"] |When `AlertMethods` is `Email`, `Phone`, or `SMS`, specify alert contact group IDs.<br><br>You can call the [ListContactGroups](https://docs.byteplus.com/en/docs/cloudmonitor/ListContactGroups) API to query contact group IDs. |
|WebhookIds |Array of String |No |["18913208\*\*\*4528"] |When `AlertMethods` is `Webhook`, specify the ID of the alert Webhook callback.<br><br>You can call the [ListWebhooks](https://docs.byteplus.com/en/docs/cloudmonitor/ListWebhooks) API to obtain Webhook callback IDs. |
|Webhook |String |No |http://alert.volc.com/callback |The Webhook callback address. This field is required when `AlertMethods` is set to `Webhook`.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Only one of the <code>WebhookIds</code> and <code>Webhook</code> parameters can be configured simultaneously.</div><br> |
|EffectStartAt |String |Yes |00:00 |The time when the policy starts taking effect. The time is in the format `HH:MM` (example: 00:00). |
|EffectEndAt |String |Yes |23:59 |The time when the alert policy stops being in effect. The time is in the format `HH:MM` (example: 23:59).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The <code>EffectEndAt</code> time must be later than the <code>EffectStartAt</code> time.</div><br> |
|ProjectName |String |Yes |default |The project to which the generated alert policy belongs. |
|UpgradePresetAlertTemplate |Boolean |No |true |Whether to upgrade the preset alert template when a new version of the preset alert template is available. Available types:<br><br><br>* **true**: Upgrades it.<br><br>* **false**: Does not upgrade it. |
|NotifyTemplates |Array of [NotifyTemplateBasic](https://docs.byteplus.com/en/docs/39/54554#notifytemplatebasic) |No |\- |Notification template configuration. |


<span id="notifytemplatebasic"></span>
### NotifyTemplateBasic


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Channel |String |No |email |Notification channel. Values:<br><br><br>* **email**: Email<br><br>* **sms**: SMS<br><br>* **phone**: Phone<br><br>* **lark**: Feishu<br><br>* **dingtalk**: DingTalk<br><br>* **wecom**: WeCom<br><br>* **slack**: Slack<br><br>* **api**: Callback address |
|NotifyTemplateId |String |No |189828\*\*\*00 |Notification template ID.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Only one notification template ID can be specified for each notification channel.</div><br> |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=EnablePresetAlertTemplate&Version=2018-01-01
Content-Type: application/json
{
    "TemplateId": "1354766247190******",
    "AlertMethods": [
        "Phone"
    ],
    "ContactGroupIds": [
        "145080093687100****"
    ],
    "EffectStartAt": "00:00",
    "EffectEndAt": "23:59",
    "ProjectName": "default",
    "UpgradePresetAlertTemplate": true,
    "NotifyTemplates": [
        {
            "Channel": "email",
            "NotifyTemplateId": "189828***00"
        }
    ]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Data |Array of String |["184361599203\*\*\*"] |A list of IDs of alert policies generated by the alert template. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "EnablePresetAlertTemplate",
        "Region": "cn-beijing",
        "Service": "cloudmonitor",
        "Version": "2018-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Data": [
            "184361599203***"
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no error codes specific to this API. For more information, see [Error codes](https://docs.byteplus.com/en/docs/cloudmonitor/Common-error-codes).

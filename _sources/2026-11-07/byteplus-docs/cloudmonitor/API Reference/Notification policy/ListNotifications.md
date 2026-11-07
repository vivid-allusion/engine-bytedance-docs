---
title: "ListNotifications"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/ListNotifications"
---

Query the list of notification policies.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions


* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=ListNotifications&Version=2018\-01\-01


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListNotifications&serviceCode=Volc_Observe&version=2018-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListNotifications |The name of the API. The API name is `ListNotifications`. |
|Version |String |Yes |2018\-01\-01 |The API version. The current API version is `2018-01-01`. |
|Name |String |No |notification\-demo |Alert notification policy name based on which filtering is performed. |
|Levels |Array of String |No |notice |Alert notification levels based on which filtering is performed. Values:<br><br><br>* **notice**<br><br>* **warning**<br><br>* **critical**<br><br>* **recovery** |
|RuleIds |Array of String |No |189898\*\*\*00 |Alert notification policy IDs based on which filtering is performed.<br><br>You can call the [ListNotifications](https://docs.byteplus.com/en/docs/cloudmonitor/ListNotifications) API to query notification policy IDs. |
|PageNumber |Integer |No |1 |Page number of the list. The default value is 1. The list range to be queried is:<br><br><br>* Actual start position = (PageNumber\-1) \* PageSize<br><br>* Actual end position = PageNumber \* PageSize |
|PageSize |Integer |No |10 |Number of rows per page for a pagination query. The default value is 10. The value must be greater than 0. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=ListNotifications&Version=2018-01-01
Content-Type: application/json
{
    "Name": "notification-demo",
    "Levels": [
        "notice"
    ],
    "RuleIds": [
        "189898***00"
    ],
    "PageNumber": 1,
    "PageSize": 10
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Data |Array of [Notification](https://docs.byteplus.com/en/docs/39/45543#notification) |\- |Notification policy details. |


<span id="notification"></span>
### Notification


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |189898\*\*\*00 |Notification policy ID. |
|Name |String |notification\-demo |Notification policy name. |
|Levels |Array of String |notice |Alert notification levels. |
|RuleIds |Array of String | |ID of the associated alert policy. |
|CreatedAt |String |2021\-10\-20T20:27:53+08:00 |The time when the notification policy was created. |
|UpdatedAt |String |2021\-10\-20T20:27:53+08:00 |The time when the notification policy was last updated. |
|EffectEndAt |String |23:59 |The time when the notification policy stops being in effect. The time is in the format HH:MM (example: 23:59). |
|EffectStartAt |String |00:00 |The time when the notification policy starts taking effect. The time is in the format `HH:MM` (example: 00:00). |
|Notifications |Array of [NotificationNotify](https://docs.byteplus.com/en/docs/39/45543#notificationnotify) |\- |Details of the notification policy for leveled alerting. |


<span id="notificationnotify"></span>
### NotificationNotify


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Level |String |critical |Alerting level. |
|WebhookIds |Array of String |18913208\*\*\*4528 |Webhook callback ID. |
|AlertMethods |Array of String |Email |Alert notification method. |
|ContactGroupIds |Array of String |145080093687100\*\*\*\* |Alert contact group ID. |
|NotifyTemplates |Array of [NotifyTemplateBasic](https://docs.byteplus.com/en/docs/39/45543#notifytemplatebasic) |\- |Notification template configuration. |


<span id="notifytemplatebasic"></span>
### NotifyTemplateBasic


|**Parameters** |**Types** |**Sample value** |**Description** |
|---|---|---|---|
|Channel |String |email |Notification channel. Values:<br><br><br>* **email**: Email<br><br>* **sms**: SMS<br><br>* **phone**: Phone call<br><br>* **lark**: Feishu<br><br>* **dingtalk**: DingTalk<br><br>* **wecom**: WeCom<br><br>* **slack**: Slack<br><br>* **api**: Callback address |
|NotifyTemplateId |String |189828\*\*\*00 |Notification template ID.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Only one notification template ID can be specified for each notification channel.</div><br> |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "ListNotifications",
        "Region": "cn-beijing",
        "Service": "cloudmonitor",
        "Version": "2018-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Data": [
            {
                "Id": "189898***00",
                "Name": "notification-demo",
                "Levels": [
                    "notice"
                ],
                "CreatedAt": "2021-10-20T20:27:53+08:00",
                "UpdatedAt": "2021-10-20T20:27:53+08:00",
                "EffectEndAt": "23:59",
                "EffectStartAt": "00:00",
                "Notifications": [
                    {
                        "Level": "critical",
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
                ]
            }
        ],
        "PageSize": 30,
        "PageNumber": 1,
        "TotalCount": 2
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no error codes specific to this API. For more information, see [Error codes](https://docs.byteplus.com/en/docs/cloudmonitor/Common-error-codes).

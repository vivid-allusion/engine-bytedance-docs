---
title: "ListWebhooks"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/ListWebhooks"
---

List alert callbacks.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions


* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=ListWebhooks&Version=2018\-01\-01


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListWebhooks&serviceCode=Volc_Observe&version=2018-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |ListWebhooks |The name of the API. The API name is `ListWebhooks`. |
|Version |String |Yes |2018\-01\-01 |The API version. The API version is `2018-01-01`. |
|Asc |Boolean |No |true |Webhook sorting order. Values:<br><br><br>* **true**: Ascending order<br><br>* **false**: Descending order |
|EventRuleId |String |No |157284163494346\*\*\*\* |Event rule ID. |
|Name |String |No |webhook\-demo |Webhook name. Fuzzy search is supported. |
|OrderBy |String |No |UpdatedAt |Webhook sorting condition. Values:<br><br><br>* **UpdatedAt**: (Default) Sorted by Webhook modification time.<br><br>* **CreatedAt**: Sorted by Webhook creation time.<br><br>* **Name**: Sorted by Webhook name. |
|PageNumber |Integer |No |1 |The page number for a pagination query. Default value: 1 |
|PageSize |Integer |No |10 |The number of rows per page for a pagination query. Default value: 10 |
|RuleId |String |No |1354766247190\*\*\*\*\*\* |Alert policy ID. |
|TotalCount |Integer |No |8 |Total number of Webhooks matching the query criteria. |
|Type |String |No |wecom |Webhook type. Values:<br><br><br>* **custom**: Custom Webhook.<br><br>* **wecom**: WeCom Webhook.<br><br>* **lark**: Feishu Webhook.<br><br>* **dingtalk**: DingTalk Webhook. |
|Url |String |No |https://qyapi.weixin.qq.com/xxxx |Webhook address. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=ListWebhooks&Version=2018-01-01
Content-Type: application/json
{
    "Name": "webhook-demo"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Data |Array of [WebhookVO](https://docs.byteplus.com/en/docs/39/29794#webhookvo) |\- |Webhook details. |


<span id="webhookvo"></span>
### WebhookVO


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Id |String |1599\*\*\*\*\*9648 |Webhook ID. |
|Url |String |https://qyapi.weixin.qq.com/xxxx |Webhook address. |
|Name |String |Webhook\-demo |Webhook name. |
|Type |String |wecom |Webhook type.<br><br><br>* **custom**: Custom Webhook.<br><br>* **wecom**: WeCom Webhook.<br><br>* **lark**: Feishu Webhook.<br><br>* **dingtalk**: DingTalk Webhook. |
|RuleIds |Array of String |1354766247190\*\*\*\*\*\* |Alert policy ID. |
|EventRuleIds |Array of String |157284163494346\*\*\*\* |Event rule ID. |
|CreatedAt |String |2021\-10\-25T18:27:24+08:00 |Webhook creation time. |
|UpdatedAt |String |2021\-10\-25T18:49:43+08:00 |Webhook update time. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "ListWebhooks",
        "Region": "cn-beijing",
        "Service": "cloudmonitor",
        "Version": "2018-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Data": [
            {
                "Id": "1599*****9648",
                "Url": "https://qyapi.weixin.qq.com/xxxx",
                "Name": "webhook-demo",
                "Type": "wecom",
                "RuleIds": [
                    "1354766247190******"
                ],
                "EventRuleIds": [
                    "157284163494346****"
                ],
                "CreatedAt": "2021-10-25T18:27:24+08:00",
                "UpdatedAt": "2021-10-25T18:49:43+08:00"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no error codes specific to this API. For more information, see [Error codes](https://docs.byteplus.com/en/docs/cloudmonitor/Common-error-codes).

&nbsp;

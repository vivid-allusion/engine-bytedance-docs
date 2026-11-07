---
title: "ListContacts"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/ListContacts"
---

Obtain the list of alert contacts.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions

Vital Managed Service for Prometheus has been deployed in multiple regions worldwide, aiming to provide you with an experience of higher stability and lower latency. You can choose an optimal access point for your service region by referring to the [Service addresses](https://docs.byteplus.com/en/docs/vmp/Service_address) topic.


* Request method: POST

* Request URL: https://vmp.cn\-beijing.byteplusapi.com.cn/?Action=ListContacts&Version=2021\-03\-03


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |ListContacts |API name. The API name is `ListContacts`. |
|Version |String |Yes |2021\-03\-03 |API version. The API version is `2021-03-03`. |
|PageNumber |Long |No |1 |Current page number, minimum or default value is 1. |
|PageSize |Long |No |10 |Results per page:<br><br><br>* A number from 0 to 100.<br><br>* The default number is 10. |
|Filter |Object of [ContactFilter](https://docs.byteplus.com/en/docs/vmp/ListContacts#contactfilter) |No |\- |Filter conditions for contact persons. |
|SortBy |String |No |CreatedAt |Whether to perform query result sorting. The value `CreatedAt` indicates that the results will be sorted. Absence of this parameter indicates no sorting. |
|SortOrder |String |No |Asc |Sorting order of query results:<br><br><br>* **Asc**: indicates sorting in ascending order.<br><br>* **Desc**: indicates sorting in descending order. |


<span id="ContactFilter"></span>
### ContactFilter


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Ids |Array of String |No |["e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c"] |Exact query by contact person IDs. |
|Name |String |No |user\-demo |Fuzzy query by the name of a contact person. |
|Email |String |No |user\-demo@example.com |Fuzzy query by the email of a contact person. |
|ContactGroupIds |Array of String |No |["e28ae750\-bbb8\-4ff4\-abf4\*\*\*"] |Fuzzy query by the contact group to which the contact belongs. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vmp.cn-beijing.byteplusapi.com.cn/?Action=CreateContact&Version=2021-03-03
Content-Type: application/json
{
    "PageNumber": 1,
    "PageSize": 10,
    "Filter": {
        "Ids": [
            "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c"
        ],
        "Name": "user-demo",
        "Email": "user-demo@example.com"
    },
    "SortBy": "CreatedAt",
    "SortOrder": "Asc"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Total |Long |100 |Total number of contacts. |
|Items |Array of [Contact](https://docs.byteplus.com/en/docs/vmp/ListContacts#contact) |\- |Contact list. |


<span id="Contact"></span>
### Contact


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Id |String |e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c |Contact person ID. |
|Name |String |user\-demo |Contact person name. |
|Email |String |user\-demo@example.com |Contact person email. |
|Webhook |Object of [Webhook](https://docs.byteplus.com/en/docs/vmp/ListContacts#webhook) |\- |Generic webhook for contacts. |
|ContactGroupIds |Array of String |["e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c"] |The contact group ID to which the contact person belongs. |
|LarkBotWebhook |Object of [LarkBotWebhook](https://docs.byteplus.com/en/docs/vmp/ListContacts#larkbotwebhook) |\- |The webhook of the Feishu group bot. |
|DingTalkBotWebhook |Object of [DingTalkBotWebhook](https://docs.byteplus.com/en/docs/vmp/ListContacts#dingtalkbotwebhook) |\- |Configurations of DingTalk robot, the contact person. |
|EmailActive |Boolean |true |Status of the contact person email:<br><br><br>* **true**: the email has been activated.<br><br>* **false**: the email has not been activated. |
|CreateTime |String |2020\-01\-01T00:00:00Z |The creation date of a contact person. It is presented in RFC3339 format. |
|WeComBotWebhook |Object of [WeComBotWebhook](https://docs.byteplus.com/en/docs/vmp/ListContacts#wecombotwebhook) |\- |The webhook of the WeCom group bot. |


<span id="Webhook"></span>
### Webhook


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Address |String |https://www.bytedance.com/ |Generic webhook address. |
|Token |String |3KSxxx |Token for generic webhook. It needs to always be used together with the generic webhook address. |


<span id="LarkBotWebhook"></span>
### LarkBotWebhook


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Address |String |https://open.feishu.cn/open\-apis/bot/v2/hook/\*\*\* |The webhook address of Larkbot. See [User Guide](https://open.feishu.cn/document/client-docs/bot-v3/bot-overview) for details. |
|SecretKey |String |6KKxxx |A webhook secret key for Larkbot. It needs to always be used together with the webhook address of Larkbot. |


<span id="DingTalkBotWebhook"></span>
### DingTalkBotWebhook


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Address |String |https://oapi.dingtalk.com/robot/send?access_token=\*\*\* |The webhook address of the DingTalk group bot.. See [User Guide](https://open.dingtalk.com/document/robots/custom-robot-access) for details. |
|SecretKey |String |SECxxx |A webhook secret key for DingTalk robot. It needs to always be used together with the webhook address of DingTalk robot. |
|AtMobiles |Array of String |["133\*\*\*\*\*\*\*\*"] |The phone number of the user who is about to be @mentioned in the group. |
|AtUserIds |Array of String |["\*\*\*\*\*\*\*\*"] |The ID of the user who is about to be @mentioned in the group. |


<span id="WeComBotWebhook"></span>
### WeComBotWebhook


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Address |String |https://qyapi.weixin.qq.com/cgi\-bin/webhook/send?key=\*\*\* |The Webhook address of WeCom robot. See [User Guide](https://developer.work.weixin.qq.com/document/path/91770) for details. |
|AtUserIds |Array of String |["\*\*\*\*\*\*\*\*"] |The ID of the user who is about to be @mentioned in the group. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1: 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListContacts",
        "Version": "2021-03-03",
        "Service": "vmp",
        "Region": "cn-beijing"
    },
    "Result": {
        "Total": 100,
        "Items": [
            {
                "Id": "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c",
                "Name": "user-demo",
                "Email": "user-demo@example.com",
                "Webhook": {
                    "Token": "3KSxxx",
                    "Address": "https://www.bytedance.com/"
                },
                "CreateTime": "2020-01-01T00:00:00Z",
                "EmailActive": true,
                "LarkBotWebhook": {
                    "Address": "https://open.feishu.cn/open-apis/bot/v2/hook/***",
                    "SecretKey": "6KKxxx"
                },
                "ContactGroupIds": [
                    "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c"
                ],
                "WeComBotWebhook": {
                    "Address": "https://qyapi.weixin.qq.com/cgi-bin/webhook/send?key=***",
                    "AtUserIds": [
                        "********"
                    ]
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
                }
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes specific to this API. For public error codes, see [Public error codes](https://docs.byteplus.com/en/docs/vmp/Common-error-codes).


|HTTP status codes |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidParameter.{{parameter}} |The specified parameter {{parameter}} is invalid. |The specified parameter is invalid. |
|403 |ProductUnsubscribed |You are not subscribed to VMP. Please go to the VMP console web page to subscribe to the service |The account is not subscribed to the VMP service. |


&nbsp;

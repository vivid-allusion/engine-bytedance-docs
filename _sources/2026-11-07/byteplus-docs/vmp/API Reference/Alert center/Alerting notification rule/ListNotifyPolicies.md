---
title: "ListNotifyPolicies"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/ListNotifyPolicies"
---

Obtain a list of alerting notification policies.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions

Vital Managed Service for Prometheus has been deployed in multiple regions worldwide, aiming to provide you with an experience of higher stability and lower latency. You can choose an optimal access point for your service region by referring to the [Service addresses](https://docs.byteplus.com/en/docs/vmp/Service_address) topic.


* Request method: POST

* Request URL: https://vmp.cn\-beijing.byteplusapi.com.cn/?Action=ListNotifyPolicies&Version=2021\-03\-03


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |ListNotifyPolicies |API name. The API name is `ListNotifyPolicies`. |
|Version |String |Yes |2021\-03\-03 |API version. The API version is` 2021-03-03`. |
|PageNumber |Long |No |1 |Current page number. The minimum and default values are both 1. |
|PageSize |Long |No |10 |Results per page:<br><br><br>* The value ranges from 0 to 100.<br><br>* The default number is 10. |
|Filter |Object of [NotifyPolicyFilter](https://docs.byteplus.com/en/docs/vmp/ListNotifyPolicies#notifypolicyfilter) |No |\- |Filter conditions of alerting notification policies. |
|SortBy |String |No |CreatedAt |Whether to perform query result sorting. The value `CreatedAt` indicates that the results will be sorted. Absence of this parameter indicates no sorting. |
|SortOrder |String |No |Asc |Sorting order of query results:<br><br><br>* **Asc**: indicates sorting in ascending order.<br><br>* **Desc**: indicates sorting in descending order. |


<span id="NotifyPolicyFilter"></span>
### NotifyPolicyFilter


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Ids |Array of String |No |["e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c"] |Exact query by IDs of alerting notification policies. |
|Name |String |No |test |Fuzzy query by the names of alerting notification policies. |
|ContactGroupIds |Array of String |No |["e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c"] |Exact query by contact group IDs. |
|ChannelNotifyTemplateIds |Array of String |No |["e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c","e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f813ad1"] |A list of IDs for custom notification templates. It helps filter alerting notification policies by template IDs. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https:://vmp.cn-beijing.byteplusapi.com.cn/?Action=ListNotifyPolicies&Version=2021-03-03
Content-Type: application/json
{
    "PageNumber": 1,
    "PageSize": 10,
    "Filter": {
        "Ids": [
            "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c"
        ],
        "Name": "test",
        "ContactGroupIds": [
            "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c"
        ]
    },
    "SortBy": "CreatedAt",
    "SortOrder": "Asc"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Total |Long |100 |Total number of alerting notification policies. |
|Items |Array of [NotifyPolicy](https://docs.byteplus.com/en/docs/vmp/ListNotifyPolicies#notifypolicy) |\- |A list of alerting notification policies. |


<span id="NotifyPolicy"></span>
### NotifyPolicy


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Id |String |e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c |Alerting notification policy ID. |
|CreateTime |String |2020\-01\-01T00:00:00Z |The creation date of the alerting notification policy. It is presented in RFC3339 format. |
|Name |String |test |Name of the alerting notification policy. |
|Description |String |This is a description |Description of the alerting notification policy. |
|Levels |Array of [NotifyPolicyLevel](https://docs.byteplus.com/en/docs/vmp/ListNotifyPolicies#notifypolicylevel) |\- |Level of alerting notification policy. |
|ChannelNotifyTemplateIds |Array of String |["e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c"] |Custom notification policy ID. |


<span id="NotifyPolicyLevel"></span>
### NotifyPolicyLevel


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Level |String |P0 |Levels of alerting notification policies. Level P0, P1, and P2 are available currently. |
|ContactGroupIds |Array of String |["e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c"] |Contact group of the alerting notify policy. |
|Channels |Array of String |["Email"] |Notification methods of alerting notification policies:<br><br><br>* **Email**: Email<br><br>* **Webhook**: Generic Webhook<br><br>* **LarkBotWebhook**: Feishu bot<br><br>* **DingTalkBotWebhook**: DingTalkBot<br><br>* **WeComBotWebhook**: WeCom Bot |
|ResolvedChannels |Array of String |["Email"] |Methods to send notifications when alerts are cleared. Available methods include:<br><br><br>* **Email**: Email<br><br>* **Webhook**: Generic Webhook<br><br>* **LarkBotWebhook**: Feishu bot<br><br>* **DingTalkBotWebhook**: DingTalkBot<br><br>* **WeComBotWebhook**: WeCom Bot |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1: 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListNotifyPolicies",
        "Version": "2021-03-03",
        "Service": "vmp",
        "Region": "cn-beijing"
    },
    "Result": {
        "Total": 100,
        "Items": [
            {
                "Id": "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c",
                "Name": "test",
                "Description": "this is a description",
                "CreateTime": "2020-01-01T00:00:00Z",
                "Levels": [
                    {
                        "Level": "P0",
                        "Channels": [
                            "Email"
                        ],
                        "ContactGroupIds": [
                            "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c"
                        ],
                        "ResolvedChannels": [
                            "Email"
                        ]
                    }
                ],
                "ChannelNotifyTemplateIds": [
                    "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c"
                ]
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The error codes for current API only are listed in the table below. See [Public error codes](https://docs.byteplus.com/en/docs/vmp/Common-error-codes) to view error codes for any APIs.


|HTTP status codes |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidParameter.{{parameter}} |The specified parameter {{parameter}} is invalid. |An invalid parameter was found. For example, an invalid workspace name was included in requests. |
|403 |ProductUnsubscribed |You are not subscribed to VMP. Please go to the VMP console web page to subscribe to the service |The account is not subscribed to the VMP Service. |


&nbsp;

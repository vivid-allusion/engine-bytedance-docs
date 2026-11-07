---
title: "UpdateNotifyPolicy"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/UpdateNotifyPolicy"
---

Update alerting notification policy.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions

Vital Managed Service for Prometheus has been deployed in multiple regions worldwide, aiming to provide you with an experience of higher stability and lower latency. You can choose an optimal access point for your service region by referring to the [Service addresses](https://docs.byteplus.com/en/docs/vmp/Service_address) topic.


* Request method: POST

* Request URL: https://vmp.cn\-beijing.byteplusapi.com.cn/?Action=UpdateNotifyPolicy&Version=2021\-03\-03


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Make sure there are no duplicate level values when multiple levels need to be configured under the parameter Levels in a single request.</div>



|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |UpdateNotifyPolicy |API name. The API name is `UpdateNotifyPolicy`. |
|Version |String |Yes |2021\-03\-03 |API version. The API version is `2021-03-03`. |
|Id |String |Yes |e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c |Alerting notification policy ID. |
|Name |String |Yes |test |Name of alerting notification policy. |
|Description |String |No |This is a description |Description of the alerting notification policy. |
|Levels |Array of [NotifyPolicyLevel](https://docs.byteplus.com/en/docs/vmp/UpdateNotifyPolicy#notifypolicylevel) |Yes |\- |Level of alerting notification policy. |
|ChannelNotifyTemplateIds |Array of String |No |["e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c"] |Custom notification template ID. |


<span id="NotifyPolicyLevel"></span>
### NotifyPolicyLevel


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Level |String |Yes |P0 |Levels of alerting notification policies. Level P0, P1, and P2 are available currently. |
|ContactGroupIds |Array of String |Yes |["e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c"] |Contact group of the alerting notification policy. |
|Channels |Array of String |Yes |["Email"] |Notification methods that alerting notification policies support:<br><br><br>* **Email**: Email<br><br>* **Webhook**: Generic webhook<br><br>* **LarkBotWebhook**: Feishu bot<br><br>* **DingTalkBotWebhook**: DingTalkBot<br><br>* **WeComBotWebhook**: WeCom bot |
|ResolvedChannels |Array of String |No |["Email"] |Methods to send notifications when alerts are cleared. Available methods include:<br><br><br>* **Email**: Email<br><br>* **Webhook**: Generic webhook<br><br>* **LarkBotWebhook**: Feishu bot<br><br>* **DingTalkBotWebhook**: DingTalkBot<br><br>* **WeComBotWebhook**: WeCom bot |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https:://vmp.cn-beijing.byteplusapi.com.cn/?Action=UpdateNotifyPolicy&Version=2021-03-03
Content-Type: application/json
{
    "Id": "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c",
    "Name": "test",
    "Description": "this is a description",
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
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Id |String |e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c |Alerting notification policy ID. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1: 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdateNotifyPolicy",
        "Version": "2021-03-03",
        "Service": "vmp",
        "Region": "cn-beijing"
    },
    "Result": {
        "Id": "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The error codes for current API only are listed in the table below. See [Public error codes](https://docs.byteplus.com/en/docs/vmp/Common-error-codes) to view error codes for any APIs.


|HTTP status codes |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidParameter.{{parameter}} |The specified parameter {{parameter}} is invalid. |An invalid parameter was found. For example, an invalid workspace name was included in requests. |
|400 |MissingParameter.{{parameter}} |The required parameter {{parameter}} is missing. |Missing necessary parameters. |
|403 |ProductUnsubscribed |You are not subscribed to VMP. Please go to the VMP console web page to subscribe to the service |The account is not subscribed to the VMP Service. |
|404 |NotFound.Id |The specified Contact/ContactGroup {{Id}} is not found. |The specified contact person/group was not found. |
|409 |Conflict.Name |The specified name conflicts with existing {{resource}}. |The specified name has already been used by an existing resource. |

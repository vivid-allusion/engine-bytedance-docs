---
title: "UpdateNotifyTemplate"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/UpdateNotifyTemplate"
---

Update alerting notification template.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions

Vital Managed Service for Prometheus has been deployed in multiple regions worldwide, aiming to provide you with an experience of higher stability and lower latency. You can choose an access point that is the most optimal for the region of your services according to the [Service addresses](https://docs.byteplus.com/en/docs/vmp/Service_address) document.


* Request method: POST

* Request URL: https://vmp.cn\-beijing.byteplusapi.com.cn/?Action=UpdateNotifyTemplate&Version=2021\-03\-03


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |UpdateNotifyTemplate |API name. The API name is `UpdateNotifyTemplate`. |
|Version |String |Yes |2021\-03\-03 |API version. The API version is `2021-03-03`. |
|Id |String |Yes |e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c |Alerting notification template ID. Alerting notification template IDs can be obtained through API [ListNotifyTemplates](https://docs.byteplus.com/en/docs/vmp/ListNotifyTemplates). |
|Name |String |No |template\-demo |Name of alerting notification template. Duplicate names are not allowed in the same region. |
|Description |String |No |This is a description |Description of alerting notification template. |
|Active |Object of [NotifyIntervalTemplate](https://docs.byteplus.com/en/docs/vmp/UpdateNotifyTemplate#notifyintervaltemplate) |No |\- |Alerting notification template. |
|Resolved |Object of [NotifyIntervalTemplate](https://docs.byteplus.com/en/docs/vmp/UpdateNotifyTemplate#notifyintervaltemplate) |No |\- |Notification template used when alerts are cleared. |


<span id="NotifyIntervalTemplate"></span>
### NotifyIntervalTemplate


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Title |String |No |An alert is triggered in the Volcano {{ .Region }} |The title of the template. |
|Content |String |Yes |**Alerting rule**: [{{ .AlertingRuleName }}]({{ .AlertingRuleDetailURL }})<br><br>**Alerting level**: {{ .Level }}<br><br>**Alerting condition**: {{ .PromQL }} {{ .Comparator }} {{ .Threshold }} [ last for {{ .For }} ] |Template content. For more details about configurations, please refer to [Lark notification template](https://docs.byteplus.com/en/docs/vmp/lark-alerting-notifacation-template) and [Structure and parameters of Variables](https://docs.byteplus.com/en/docs/vmp/variable-structure-and-parameters). |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vmp.cn-beijing.byteplusapi.com.cn?Action=UpdateNotifyTemplate&Version=2021-03-03
Content-Type: application/json
{
    "Id": "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c",
    "Name": "template-demo",
    "Description": "This is a description",
    "Active": {
        "Title": "An alert is triggered in {{ .Region }}",
        "Content": "**Alerting rule**: [{{ .AlertingRuleName }}]({{ .AlertingRuleDetailURL }})\n**Alerting level**: {{ .Level }}\n**Alerting condition**: {{ .PromQL }} {{ .Comparator }} {{ .Threshold }} [ last for {{ .For }} ]"
    },
    "Resolved": {
        "Title": "An alert is triggered in {{ .Region }}",
        "Content": "**Alerting rule**: [{{ .AlertingRuleName }}]({{ .AlertingRuleDetailURL }})\n**Alerting level**: {{ .Level }}\n**Alerting condition**: {{ .PromQL }} {{ .Comparator }} {{ .Threshold }} [ last for {{ .For }} ]"
    }
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Id |String |e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c |Alerting notification template ID. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1: 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdateNotifyTemplate",
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

The error codes for current API only are listed in the table below. See[ Public error codes](https://docs.byteplus.com/en/docs/vmp/Common-error-codes) to view error codes for any APIs.


|HTTP status codes |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidParameter.{{parameter}} |The specified parameter {{parameter}} is invalid. |The specified parameter is invalid. |
|400 |MissingParameter.{{parameter}} |The required parameter {{parameter}} is missing. |Missing necessary parameters. |
|403 |ProductUnsubscribed |You are not subscribed to VMP. Please go to the VMP console web page to subscribe to the service |The account is not subscribed to the VMP Service. |
|404 |NotFound.Id |The specified Contact/ContactGroup {{Id}} is not found. |The specified contact person/group was not found. |
|409 |Conflict.Name |The specified name conflicts with existing {{resource}}. |The specified name has already been used by an existing resource. |

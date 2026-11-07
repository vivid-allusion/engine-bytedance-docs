---
title: "ListNotifyTemplates"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/ListNotifyTemplates"
---

Obtain alert notification templates.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions

Vital Managed Service for Prometheus has been deployed in multiple regions worldwide, aiming to provide you with an experience of higher stability and lower latency. You can choose an access point that is the most optimal for the region of your services according to the [Service addresses](https://docs.byteplus.com/en/docs/vmp/Service_address) document.


* Request method: POST

* Request URL: https://vmp.cn\-beijing.byteplusapi.com.cn/?Action=ListNotifyTemplates&Version=2021\-03\-03


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |ListNotifyTemplates |API name. The API name is `ListNotifyTemplates`. |
|Version |String |Yes |2021\-03\-03 |API version. The API version is `2021-03-03`. |
|PageNumber |Long |No |1 |Current page number. The minimum and default values are both 1. |
|PageSize |Long |No |10 |Results per page. It is an integer from 0 to 100. The default number is 10. |
|Filter |Object of [NotifyTemplateFilter](https://docs.byteplus.com/en/docs/vmp/ListNotifyTemplates#notifytemplatefilter) |No |\- |Filter condition. |
|SortBy |String |No |CreatedAt |Whether to perform query result sorting.The value `CreatedAt` indicates that the results will be sorted. Absence of this parameter indicates no sorting. |
|SortOrder |String |No |Asc |Sorting order of query results:<br><br><br>* **Asc**: indicates sorting in ascending order.<br><br>* **Desc**: indicates sorting in descending order. |


<span id="NotifyTemplateFilter"></span>
### NotifyTemplateFilter


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Ids |Array of String |No |["e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c"] |Exact query by IDs. |
|Name |String |No |template\-demo |Fuzzy query by names. |
|Channel |String |No |LarkBot |Exact query by channels. Valid values:<br><br><br>* **LarkBotWebhook**: Alert notification template for Lark.<br><br>* **DingTalkBotWebhook**: Alert notification template for DingTalk.<br><br>* **WeComBotWebhook**: Alerttification template for WeCom |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vmp.cn-beijing.byteplusapi.com.cn/?Action=ListNotifyTemplates&Version=2021-03-03
Content-Type: application/json
{
    "PageNumber": 1,
    "PageSize": 10,
    "Filter": {
        "Ids": [
            "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c"
        ],
        "Name": "template-demo",
        "Channel": "LarkBot"
    },
    "SortBy": "CreatedAt",
    "SortOrder": "Asc"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Total |Long |100 |Total number of query results. |
|Items |Array of [NotifyTemplate](https://docs.byteplus.com/en/docs/vmp/ListNotifyTemplates#notifytemplate) |\- |A list of query results. |


<span id="NotifyTemplate"></span>
### NotifyTemplate


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Id |String |test |Alert notification template ID. |
|Name |String |test |Name of alert notification template. |
|Active |Object of [NotifyIntervalTemplate](https://docs.byteplus.com/en/docs/vmp/ListNotifyTemplates#notifyintervaltemplate) |\- |Alert notification template. |
|Channel |String |LarkBotWebhook |Alert notification channel. |
|Resolved |Object of [NotifyIntervalTemplate](https://docs.byteplus.com/en/docs/vmp/ListNotifyTemplates#notifyintervaltemplate) |\- |Notification template used when alerts are cleared. |
|CreateTime |String |2020\-01\-01T00:00:00Z |The creation date of the alert notification template. |
|UpdateTime |String |2020\-01\-01T00:00:00Z |The update date of the alert notification template. |
|Description |String |This is a description |Description of alert notification template. |


<span id="NotifyIntervalTemplate"></span>
### NotifyIntervalTemplate


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Title |String |An alert has been raised in the {{ .Region }} of BytePlus |Template title. |
|Content |String |**Alerting rule**: [{{ .AlertingRuleName }}]({{ .AlertingRuleDetailURL }})<br><br>**Alerting level**: {{ .Level }}<br><br>**Alerting condition**: {{ .PromQL }} {{ .Comparator }} {{ .Threshold }} [ last for {{ .For }} ] |Template content. For more details about configurations, please refer to [Lark notification template](https://docs.byteplus.com/en/docs/vmp/lark-alerting-notifacation-template) and [Structure and parameters of Variables](https://docs.byteplus.com/en/docs/vmp/variable-structure-and-parameters). |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1: 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListNotifyTemplates",
        "Version": "2021-03-03",
        "Service": "vmp",
        "Region": "cn-beijing"
    },
    "Result": {
        "Total": 100,
        "Items": [
            {
                "Id": "test",
                "Name": "test",
                "Active": {
                    "Title": "An alert has been raised in the {{ .Region }}",
                    "Content": "**Alerting rule**: [{{ .AlertingRuleName }}]({{ .AlertingRuleDetailURL }})\n**Alerting level**: {{ .Level }}\n**Alerting condition**: {{ .PromQL }} {{ .Comparator }} {{ .Threshold }} [ last for {{ .For }} ]"
                },
                "Channel": "LarkBotWebhook",
                "Resolved": {
                    "Title": "Alert in the {{ .Region }} is cleared",
                    "Content": "**Alerting rule**: [{{ .AlertingRuleName }}]({{ .AlertingRuleDetailURL }})\n**Alerting level**: {{ .Level }}\n**Alerting condition**: {{ .PromQL }} {{ .Comparator }} {{ .Threshold }} [ last for {{ .For }} ]"
                },
                "CreateTime": "2020-01-01T00:00:00Z",
                "UpdateTime": "2020-01-01T00:00:00Z",
                "Description": "This is a description"
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
|400 |InvalidParameter.{{parameter}} |The specified parameter {{parameter}} is invalid. |The specified parameter is invalid. |
|400 |MissingParameter.{{parameter}} |The required parameter {{parameter}} is missing. |Missing necessary parameters. |
|403 |ProductUnsubscribed |You are not subscribed to VMP. Please go to the VMP console web page to subscribe to the service |The account is not subscribed to the VMP Service. |

---
title: "ListNotifyTemplates"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/ListNotifyTemplates"
---

Query the list of notification templates.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions


* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=ListNotifyTemplates&Version=2018\-01\-01


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListNotifyTemplates&serviceCode=Volc_Observe&version=2018-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListNotifyTemplates |The name of the API. The API name is `ListNotifyTemplates`. |
|Version |String |Yes |2018\-01\-01 |The API version. The current API version is `2018-01-01`. |
|Name |String |No |template\-demo |Notification template name.<br><br><br>* It is a string that can contain Chinese characters, uppercase letters, lowercase letters, and special characters.<br><br>* It cannot start with a digit, a hyphen (`-`), or other special characters.<br><br>* It must be 1 to 128 characters in length. |
|Ids |Array of String |No |189828\*\*\*00 |Notification template ID. |
|Types |Array of String |No |metric |Notification template type. Valid values:<br><br><br>* **metric**: Alert notification template.<br><br>* **event**: Event notification template. |
|Channels |Array of String |No |email |Notification channel. Values:<br><br><br>* **email**: Email<br><br>* **sms**: SMS<br><br>* **phone**: Phone call<br><br>* **lark**: Feishu<br><br>* **dingtalk**: DingTalk<br><br>* **wecom**: WeCom<br><br>* **slack**: Slack<br><br>* **api**: Callback address |
|PageNumber |Integer |No |1 |The page number for a pagination query. The default value is 1.<br><br><br>* Actual start position = (PageNumber\-1) \* PageSize<br><br>* Actual end position = PageNumber \* PageSize |
|PageSize |Integer |No |30 |The number of rows per page for a pagination query. The default value is 30. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=ListNotifyTemplates&Version=2018-01-01
Content-Type: application/json
{
    "Name": "template-demo",
    "Ids": [
        "189828***00"
    ],
    "Types": [
        "metric"
    ],
    "Channels": [
        "email"
    ],
    "PageNumber": 1,
    "PageSize": 30
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Data |Array of [NotifyTemplate](https://docs.byteplus.com/en/docs/39/63270#notifytemplate) |\- |The notification template details. |


<span id="notifytemplate"></span>
### NotifyTemplate


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |189828\*\*\*00 |Notification template ID. |
|Name |String |template\-demo |Notification template name. |
|Description |String |this is a template\-demo |Description of the notification template. |
|Type |String |metric |Notification template type. Valid values:<br><br><br>* **metric**: Alert notification template.<br><br>* **event**: Event notification template. |
|Channel |String |email |Notification channel. Values:<br><br><br>* **email**: Email<br><br>* **sms**: SMS<br><br>* **phone**: Phone call<br><br>* **lark**: Feishu<br><br>* **dingtalk**: DingTalk<br><br>* **wecom**: WeCom<br><br>* **slack**: Slack<br><br>* **api**: Callback address |
|Title |String |[{{ .Level \| translate "Level" "en" }}] [{{ translate "Type" "en" .Type }}] Platform Account {{ .AccountName }}({{ .AccountId }})'s alert policy "{{ .RuleName }}" {{ if (contains "Recovered" .Type) }} has recovered{{ else }} has triggered a {{ .Level \| translate "Level" "en" }} level alert{{ end }} |Title of the notification template. |
|Content |String |**Alert message**:<br><br>Alert type: {{ .Type }}<br><br>Account name: {{ .AccountName }}<br><br>Account ID: {{ .AccountId }}<br><br>Alert policy name: {{ .RuleName }}<br><br>Alert policy ID: {{ .RuleId }}<br><br>Alert policy details: {{ .RuleURL }} |Notification template content. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "ListNotifyTemplates",
        "Region": "cn-beijing",
        "Service": "cloudmonitor",
        "Version": "2018-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Data": [
            {
                "Id": "189828***00",
                "Name": "template-demo",
                "Description": "this is a template-demo",
                "Type": "metric",
                "Title": "[{{ .Level | translate \"Level\" \"en\" }}] [{{ translate \"Type\" \"en\" .Type }}] Alert policy \"{{ .RuleName }}\" for platform account {{ .AccountName }}({{ .AccountId }}) {{ if (contains \"Recovered\" .Type) }}has recovered{{ else }}has triggered a {{ .Level | translate \"Level\" \"en\" }} level alert{{ end }}",
                "Channel": "email",
                "Content": "**Alert Information**:\n\nAlert Type: {{ .Type }}\nAccount Name: {{ .AccountName }}\nAccount ID: {{ .AccountId }}\nAlert Policy Name: {{ .RuleName }}\nAlert Policy ID: {{ .RuleId }}\nAlert Policy Details: {{ .RuleURL }}"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no error codes specific to this API. For more information, see [Error codes](https://docs.byteplus.com/en/docs/cloudmonitor/Common-error-codes).

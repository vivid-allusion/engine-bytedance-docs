---
title: "ListDefaultNotifyTemplates"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/ListDefaultNotifyTemplates"
---

Query the list of default notification templates.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions


* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=ListDefaultNotifyTemplates&Version=2018\-01\-01


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListDefaultNotifyTemplates&serviceCode=Volc_Observe&version=2018-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListDefaultNotifyTemplates |The name of the API. The API name is `ListDefaultNotifyTemplates`. |
|Version |String |Yes |2018\-01\-01 |The API version. The current API version is `2018-01-01`. |
|Type |String |Yes |metric |Notification template type. Valid values:<br><br><br>* **metric**: Alert notification template.<br><br>* **event**: Event notification template. |
|Channels |Array of String |No |email |Notification channel. Values:<br><br><br>* **email**: Email<br><br>* **sms**: SMS<br><br>* **phone**: Phone call<br><br>* **lark**: Feishu<br><br>* **dingtalk**: DingTalk<br><br>* **wecom**: WeCom<br><br>* **slack**: Slack<br><br>* **api**: Callback address |
|Language |String |No |zh |Language of the notification template. Values:<br><br><br>* **zh**: Chinese<br><br>* **en**: English |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=ListDefaultNotifyTemplates&Version=2018-01-01
Content-Type: application/json
{
    "Type": "metric",
    "Channels": [
        "email"
    ],
    "Language": "zh"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Data |Array of [DefaultNotifyTemplate](https://docs.byteplus.com/en/docs/39/63269#defaultnotifytemplate) |\- |Details of the default notification template. |


<span id="defaultnotifytemplate"></span>
### DefaultNotifyTemplate


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Type |String |alert |Notification template type. Valid values:<br><br><br>* **alert**: Alert notification template.<br><br>* **event**: Event notification template. |
|Channel |String |email |Notification channel. Values:<br><br><br>* **email**: Email<br><br>* **sms**: SMS<br><br>* **phone**: Phone call<br><br>* **lark**: Feishu<br><br>* **dingtalk**: DingTalk<br><br>* **wecom**: WeCom<br><br>* **slack**: Slack<br><br>* **api**: Callback address |
|Language |String |zh |Language of the notification template. Values:<br><br><br>* **zh**: Chinese<br><br>* **en**: English |
|Title |String |[{{ .Level \| translate "Level" "en" }}] [{{ translate "Type" "en" .Type }}] Platform Account {{ .AccountName }}({{ .AccountId }})'s alert policy "{{ .RuleName }}" {{ if (contains "Recovered" .Type) }} has recovered{{ else }} has triggered a {{ .Level \| translate "Level" "en" }} level alert{{ end }} |Title of the notification template. |
|Content |String |**Alert message**:<br><br>Alert type: {{ .Type }}<br><br>Account name: {{ .AccountName }}<br><br>Account ID: {{ .AccountId }}<br><br>Alert policy name: {{ .RuleName }}<br><br>Alert policy ID: {{ .RuleId }}<br><br>Alert policy details: {{ .RuleURL }} |Notification template content. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "ListDefaultNotifyTemplates",
        "Region": "cn-beijing",
        "Service": "cloudmonitor",
        "Version": "2018-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Data": [
            {
                "Type": "alert",
                "Channel": "email",
                "Language": "en",
                "Title": "[{{ .Level | translate \"Level\" \"en\" }}] [{{ translate \"Type\" \"en\" .Type }}] Alert policy \"{{ .RuleName }}\" for platform account {{ .AccountName }}({{ .AccountId }}) {{ if (contains \"Recovered\" .Type) }}has recovered{{ else }}has triggered a {{ .Level | translate \"Level\" \"en\" }} level alert{{ end }}",
                "Content": "**Alert Information**:\n\nAlert Type: {{ .Type }}\nAccount Name: {{ .AccountName }}\nAccount ID: {{ .AccountId }}\nAlert Policy Name: {{ .RuleName }}\nAlert Policy ID: {{ .RuleId }}\nAlert Policy Details: {{ .RuleURL }}"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no error codes specific to this API. For more information, see [Error codes](https://docs.byteplus.com/en/docs/cloudmonitor/Common-error-codes).

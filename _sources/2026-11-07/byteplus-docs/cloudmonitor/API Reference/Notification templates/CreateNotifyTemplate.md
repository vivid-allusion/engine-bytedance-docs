---
title: "CreateNotifyTemplate"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/CreateNotifyTemplate"
---

Create a notification template.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions


* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=CreateNotifyTemplate&Version=2018\-01\-01


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateNotifyTemplate&serviceCode=Volc_Observe&version=2018-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |CreateNotifyTemplate |The name of the API. The API name is `CreateNotifyTemplate`. |
|Version |String |Yes |2018\-01\-01 |The API version. The current API version is `2018-01-01`. |
|Name |String |Yes |template\-demo |Notification template name.<br><br><br>* It is a string that can contain Chinese characters, uppercase letters, lowercase letters, and special characters.<br><br>* It cannot start with a digit, a hyphen (`-`), or other special characters.<br><br>* It must be 1 to 128 characters in length. |
|Description |String |No |this is a template\-demo |Description of the notification template.<br><br><br>* It is a string that can contain Chinese characters, uppercase letters, lowercase letters, and special characters.<br><br>* It must be 0 to 255 characters in length. |
|Type |String |Yes |metric |Notification template type. Valid values:<br><br><br>* **metric**: Alert notification template.<br><br>* **event**: Event notification template. |
|Channel |String |Yes |email |Notification channel. Values:<br><br><br>* **email**: Email<br><br>* **sms**: SMS<br><br>* **phone**: Phone call<br><br>* **lark**: Feishu<br><br>* **dingtalk**: DingTalk<br><br>* **wecom**: WeCom<br><br>* **slack**: Slack<br><br>* **api**: Callback address |
|Title |String |No |[{{ .Level \| translate "Level" "zh" }}] [{{ translate "Type" "zh" .Type }}] Platform Account {{ .AccountName }}({{ .AccountId }})'s alert policy "{{ .RuleName }}" {{ if (contains "Recovered" .Type) }} has recovered{{ else }} has triggered a {{ .Level \| translate "Level" "zh" }} level alert{{ end }} |The title of the notification template. This field is required only when `Channel` is set to `email`, `lark`, `dingtalk`, `wecom`, or `slack`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Notification templates support writing and rendering notification content using Markdown syntax and Go Template syntax. For details, see <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Template_syntax_overview">Template syntax overview</a> and <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Extension_functions_and_variables">Extension functions and variables</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The character limit for this field varies depending on the notification channel. For details, see <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Creating_a_notification_template">Creating notification templates</a>.</div><br> |
|Content |String |Yes |**Alert message**:<br><br>Alert type: {{ .Type }}<br><br>Account name: {{ .AccountName }}<br><br>Account ID: {{ .AccountId }}<br><br>Alert policy name: {{ .RuleName }}<br><br>Alert policy ID: {{ .RuleId }}<br><br>Alert policy details: {{ .RuleURL }} |Notification template content.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Notification templates support writing and rendering notification content using Markdown syntax and Go Template syntax. For details, see <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Template_syntax_overview">Template syntax overview</a> and <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Extension_functions_and_variables">Extension functions and variables</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The character limit for this field varies depending on the notification channel. For details, see <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Creating_a_notification_template">Creating notification templates</a>.</div><br> |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=CreateNotifyTemplate&Version=2018-01-01
Content-Type: application/json
{
    "Channel": "email",
    "Content": "**Alert Information**:\n\nAlert Type: {{ .Type }}\nAccount Name: {{ .AccountName }}\nAccount ID: {{ .AccountId }}\nAlert Policy Name: {{ .RuleName }}\nAlert Policy ID: {{ .RuleId }}\nAlert Policy Details: {{ .RuleURL }}",
    "Description": "this is a template-demo",
    "Name": "template-demo",
    "Title": "[{{ .Level | translate \"Level\" \"en\" }}] [{{ translate \"Type\" \"en\" .Type }}] Alert policy \"{{ .RuleName }}\" for platform account {{ .AccountName }}({{ .AccountId }}) {{ if (contains \"Recovered\" .Type) }}has recovered{{ else }}has triggered a {{ .Level | translate \"Level\" \"en\" }} level alert{{ end }}",
    "Type": "metric"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Data |String |189828\*\*\*00 |Notification template ID. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "CreateNotifyTemplate",
        "Region": "cn-beijing",
        "Service": "cloudmonitor",
        "Version": "2018-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Data": "189828***00"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no error codes specific to this API. For more information, see [Error codes](https://docs.byteplus.com/en/docs/cloudmonitor/Common-error-codes).

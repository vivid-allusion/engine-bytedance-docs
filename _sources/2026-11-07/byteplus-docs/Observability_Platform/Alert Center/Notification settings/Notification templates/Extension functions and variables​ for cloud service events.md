---
title: "Extension functions and variables​ for cloud service events"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Extension_functions_and_variables"
---

You can use preset alert variables in notification templates. This topic describes the structure and parameters of preset alert variables for cloud service events.

<span id="EmhjqLtf"></span>
## Extension functions

Notification templates support Go Template built\-in functions and extension functions. The following table provides the details.


|Function |Description |
|---|---|
|Go Template built\-in functions |Notification templates support Go Template built\-in functions. For details, see the [official documentation](https://pkg.go.dev/text/template). |
|translate<br><br> |Translate the variable value into natural language.<br><br>translate(type string, lang string, val string) string<br><br><br>* type: Variable name<br><br>   * Alert templates: Support the `Region`, `Type`, `Level`, and `Namespace` variables.<br><br>   * Event templates: Support the `Region`, `Type`, `Level`, `Source`, and `Event` variables.<br><br>* Lang: The target language of conversion. Supported languages include `zh` (Chinese) and `en` (English).<br><br>* val: Variable value. |
|Integer calculation functions |* Sum: add(i ...interface{}) int64<br><br>* Subtraction: sub(a, b interface{}) int64<br><br>* Maximum: max(a interface{}, i ...interface{}) int64<br><br>* Minimum: min(a interface{}, i ...interface{}) int64 |
|Collection operation functions |Slicing<br><br><br>* slice(list interface{}, indices ...int) interface{}<br><br><br>map<br><br><br>* get(m map[string]interface{}, key string) interface{} |
|String functions |* Truncate a string: trunc(c int, s string) string<br><br>* Get a substr: substr(start int, end int, s string) string<br><br>* Trim whitespaces: trim(s string) string<br><br>* Check whether a substr is present: contains(substr string, str string) bool<br><br>* Check whether a prefix is present: hasPrefix(substr string, str string) bool<br><br>* Check whether a suffix is present: hasSuffix(substr string, str string) bool<br><br>* Escape a string: quote(str ...interface{}) string<br><br>* Join strings: join(sep string, v interface{}) string<br><br>* Replace characters: replace(old string, new string, src string) string<br><br>* Format as a string: toString(v interface{}) string |
|Time functions |* If the variable is of type `time.Time`, you can use the time function `.Format` to define the time format. For example, `{{ .HappenedAt.Format "2006-01-02 15:04:05(UTCZ07:00)" }}`. |
|JSON operations |* JSON: toJson(v interface{}) string<br><br>* PrettyJSON: toPrettyJson(v interface{}) string |


<span id="wMvWNoHo"></span>
## Data structure

This topic uses the following JSON example to demonstrate the variables, parameters, and data structures supported by cloud service event templates. This helps you understand common Go template syntax and its usage.

<span id="U0yvHHe4"></span>
## Variable description

<div data-tips="true" data-tips-type="default">Description</div>



* <div data-tips="true" data-tips-type="default">You can use the standard Go Template approach to get values of non\-nested variables. For example, you can use <code>{{ .Region }}</code>.</div>


* <div data-tips="true" data-tips-type="default">For nested variables, you need to use custom variables to obtain all resources. For example, you define the <code>$rule</code> variable and use iteration to get all resources: <code>{{ range $idx, $rule := .Rules }}</code>. For internal variables, you need to use <code>$rule.fieldName </code>(for example, <code>{{ $rule.RuleId }}</code>) to get variable values.</div>



The following table provides the parameters and descriptions of preset variables that can be used in a notification template.


|Variable name |Type |Description |Sample value |Example |
|---|---|---|---|---|
|Type |String |Alert type. The value is `Event`. |Event |* Render it directly: `{{ .Type }}`<br><br>* Use the extension function to translate it into natural language: `{{ translate "Type" "zh"  .Type }}`. For example, render `Event` as `event` **.**  |
|SiteName |String |Site name. |Cloud Monitor |`{{ .SiteName }}` |
|AccountName |String |Account name. |user\-demo |`{{ .AccountName }}` |
|AccountId |String |Account ID. |21000\*\*\*\*\* |`{{ .AccountId }}` |
|Source |String |Event source. |ecs |* Render it directly: `{{ .Source }}`<br><br>* Use the extension function to translate it into natural language`: {{ translate "Source" "zh" .Source }}`. For example, render `ecs` as `Elastic Compute Service`. |
|Level |String |Event level. Possible values:<br><br><br>* **critical**<br><br>* **warning**<br><br>* **notice**<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If multiple rules are matched, the highest level is applied.</div><br> |critical |* Render it directly: `{{ .Level }}`<br><br>* Use the extension function to translate into natural language: `{{ translate "Level" "zh" .Level }}`. For example, render `critical` as `Serious`. |
|Id |String |Event ID. |1803\*\*\*\*\*\* |`{{ .Id }}` |
|Event |String |Event type. |ecs:Instance:RebootInstance.Executing |* Render it directly: `{{ .Event }}`<br><br>* Translate into natural language: `{{ translate "Event" "zh" .Event }}`. For example, render `ecs:Instance:RebootInstance.Executing` as `Instance restart: Executing`. |
|HappenedAt |time.Time |The time when the event occurs. |2025\-01\-01 00:00:00(UTC+08:00) |Format the time: `{{ .HappenedAt.Format "2006-01-02 15:04:05(UTCZ07:00)" }}` |
|Region |String |Region of the cloud product resource. |cn\-beijing |* Render it directly: `{{ .Region }}`<br><br>* Use the extension function to translate into natural language: `{{ translate "Region" "zh" .Region }}`. For example, render `cn-beijing` as `China (Beijing)`. |
|ResourceId |String |Cloud product resource ID. |i\-yd9j\*\*\*\*\* |`{{ .ResourceId }}` |
|ResourceName |String |Cloud product resource name. |ecs\-demo |`{{ .ResourceName }}` |
|ProjectName |String |Name of the project to which the cloud product resource belongs. |default |`{{ .Project }}` |
|TagSet |Array of Tag |Cloud product resource tags. Each tag consists of a `Key` and `Value`. |\- |Iterate through tags:<br><br>```Go```<br>```{{ range $idx, $tag := .Tags }}```<br>```{{ $tag.Key }}: {{ $tag.Value }}```<br>```{{ end }}```<br> |
|Details |map[string]interface{} |Event details.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Event formats vary across different cloud products.</div><br> |\- |Iterate through details:<br><br>```Go```<br>```{{ range $key, $val := .Details }}```<br>```{{ $key }}: {{ $val }}```<br>```{{ end }}```<br> |
|Rules |Array of EventRule |A list of matched event rules. |\- |Iterate through rules:<br><br>```Go```<br>```{{ range $idx, $rule := .Rules }}```<br>```{{ $rule.RuleName }} ({{ $rule.Level }})```<br>```{{ end }}```<br> |
|HistoryURL |String |URL to the Event Center. |https://console.byteplus.com/observe/cloud\-monitor/alert/history |`{{ .HistoryURL }}` |


<span id="fZpDNhM5"></span>
### EventRule


|Variable name |Type |Description |Sample value |Example |
|---|---|---|---|---|
|RuleId |String |Event rule ID. |19251\*\*\*\* |`{{ $rule.RuleId }}` |
|RuleName |String |Event rule name. |event\-demo |`{{ $rule.RuleName }}` |
|Level |String |Event rule level. Possible values:<br><br><br>* **critical**<br><br>* **warning**<br><br>* **notice** |critical |* Render it directly: `{{ $rule.Level }}`<br><br>* Use the extension function to translate into natural language: `{{ translate "Level" "zh" $rule.Level }}`. For example, render `critical` as `Serious`. |
|RuleURL |String |URL to the event rule. |https://console.byteplus.com/observe/cloud\-monitor/event/rules/detail?id=1790\*\*\*\* |`{{ $rule.RuleURL }}` |


<span id="OJgMlVha"></span>
## Configuration example

In addition to the preset event templates, you can specify custom content of a notification template based on the data structures of alert variables, Go Template syntax, and Markdown syntax. This section provides a configuration example.

```Markdown
**Event Information**:

---

Alert Type: {{ .Type }}
Account Name: {{ .AccountName }}
Account ID: {{ .AccountId }}
Event Source: {{ .Source }}
Event Level: {{ .Level }}
Event ID: {{ .Id }}
Event Type: {{ .Event }}
Event Occurrence Time: {{ .HappenedAt }}
Cloud Product Region: {{ .Region }}
Cloud Product Resource ID: {{ .ResourceId }}
Cloud Product Resource Name: {{ .ResourceName }}
Event Center Link: {{ .HistoryURL }}

---

**Details of Resources Triggering the Event**:
{{- range $key, $val := .Details }}
{{ $key }}: {{ $val }}
{{- end }}
```

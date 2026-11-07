---
title: "Extension functions and variables"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Extension_functions_and_variables"
---

You can use preset alert variables in notification templates. This topic describes the structure and parameters of preset alert variables.

<span id="jdkYLRBh"></span>
## Extension functions

Cloud Monitor notification templates support built\-in Go Template functions and extension functions. The following table provides the details.


|Function |Descriptions |
|---|---|
|Go Template built\-in functions |Cloud Monitor notification templates support Go Template built\-in functions. For details, see the [official documentation](https://pkg.go.dev/text/template). |
|translate<br><br> |Translate the variable value into natural language.<br><br>translate(type string, lang string, val string) string<br><br><br>* type: Variable name<br><br>   * Alert templates: Supported variables include `Region`, `Type`, `Level`, and `Namespace`.<br><br>   * Event templates: Supported variables include `Region`, `Type`, `Level`, `Source`, and `Event`.<br><br>* Lang: The target language of conversion. Supported languages include `zh` (Chinese) and `en` (English).<br><br>* val: Variable value. |
|Integer calculation functions |* Sum: add(i ...interface{}) int64<br><br>* Subtraction: sub(a, b interface{}) int64<br><br>* Maximum: max(a interface{}, i ...interface{}) int64<br><br>* Minimum: min(a interface{}, i ...interface{}) int64 |
|Collection operation functions |Slicing<br><br><br>* slice(list interface{}, indices ...int) interface{}<br><br><br>map<br><br><br>* get(m map[string]interface{}, key string) interface{} |
|String functions |* Truncate a string: trunc(c int, s string) string<br><br>* Get a substr: substr(start int, end int, s string) string<br><br>* Trim whitespaces: trim(s string) string<br><br>* Check whether a substr is present: contains(substr string, str string) bool<br><br>* Check whether a prefix is present: hasPrefix(substr string, str string) bool<br><br>* Check whether a suffix is present: hasSuffix(substr string, str string) bool<br><br>* Escape a string: quote(str ...interface{}) string<br><br>* Join strings: join(sep string, v interface{}) string<br><br>* Replace characters: replace(old string, new string, src string) string<br><br>* Format as a string: toString(v interface{}) string |
|Time functions |* If the variable is of type `time.Time`, you can use the time function `.Format` to define the time format. For example, `{{ .HappenedAt.Format "2006-01-02 15:04:05(UTCZ07:00)" }}`. |
|JSON operations |* JSON: toJson(v interface{}) string<br><br>* PrettyJSON: toPrettyJson(v interface{}) string |


<span id="zFuqAveh"></span>
## Alert template variables

<span id="QxA6Yw8s"></span>
### Data structure

The following JSON example demonstrates variables, parameters, and data structures supported in Cloud Monitor alert templates. This helps you understand common Go template syntax and its usage.

```json
{
        "MaxCount": 5,
        "Type": "Metric",
        "SiteName": "CloudMonitor",
        "AccountName": "user-demo",
        "AccountId": "21000*****",
        "RuleName": "alert-demo",
        "RuleId": "19251*****",
        "RuleURL": "https://console.byteplus.com/observe/cloud-monitor/alert/strategy?id=19251*****",
        "RuleType": "static",
        "Namespace": "VCM_ECS",
        "SubNamespace": "Instance",
        "Region": "cn-beijing",
        "HappenedAt": "2025-01-02 00:00:00(UTC+08:00)",
        "RuleCondition": "The average QPS has increased or decreased by 0% in link relative ratio compared with the previous period, lasting for 10 periods (1 period = 1 minute).",
        "Level": "critical",
        "ProjectName": "default",
        "TagSet": [
          {
             "Key": "test",
             "Value": "test"
          }
        ],
        "Resources": [
          {
             "AlertGroupId": "67fd19******",
             "AlertGroupURL": "https://console.byteplus.com/observe/cloud-monitor/alert/history/detail?id=67fd19*****",
             "Id": "i-yd9j*****",
             "Name": "ecs-demo",
             "DetailURL": "https://console.byteplus.com/observe/cloud-monitor/product/*******",
             "Region": "cn-beijing",
             "FirstAlertTime": "2025-07-06 00:00:00(UTC+08:00)",
             "LastAlertTime": "2025-07-07 00:00:00(UTC+08:00)",
             "LastSendLevel": "warning",
             "Metrics": [
               {
                  "Name": "CpuTotal",
                  "Unit": "%",
                  "Threshold": "80",
                  "CurrentValue": "90",
                  "Description": "CPU usage",
                  "Warn": "true",
                  "IsTimeCompare": "true",
                  "InherentUnit": "%",
                  "LastValue": "85",
                  "LastDescription": "CPU usage in the last period",
                  "CurrentValue": "91",
                  "CurrentDescription": "Current CPU usage"
               }
            ],
            "Dimensions": [
              {
                 "Name": "ResourceID",
                 "Value": "i-yd9j*****",
                 "Description": "Instance ID"
              }
            ],
            "ProjectName": "default",
            "TagSet": [
              {
                 "Key": "test",
                 "Value": "test"
              }
            ],
            "Metadatas": [
              {
                 "Name": "IP.Inside",
                 "Value": "192.168.0.1",
                 "Description": "Private IP address"
              }
            ]
          }
        ], 
        "HistoryURL": "https://console.byteplus.com/observe/cloud-monitor/alert/history",
        "CreateSilenceURL": "https://console.byteplus.com/observe/cloud-monitor/notice/silencePolicy/create?ruleId=19251*****"
}
```


<span id="WAjk0iiA"></span>
### Variable description

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">You can use the standard Go Template approach to get values of non\-nested variables. For example, you can use <code>{{ .Region }}</code>.</div>


* <div data-tips="true" data-tips-type="default">For nested variables, you need to use custom variables to obtain all resources. For example, you define the <code>$resource</code> variable and use iteration to get all resources: <code>{{ range $idx, $resource := .Resources }}</code>. For internal variables, you need to use <code>$resource.fieldName</code> (for example, <code>{{ $resource.Id }}</code>) to get variable values.</div>



The following table provides the parameters and descriptions of preset variables that can be used in a notification template.


|Variable name |Type |Descriptio |Sample value |Example |
|---|---|---|---|---|
|MaxCount |Int |Maximum number of resources rendered by the alert template for the current sending channel. |5 |`{{ .MaxCount }}` |
|Type |String |Alert type. Possible values:<br><br><br>* **Metric**: Alert<br><br>* **MetricRecovered**: Alert recovery<br><br>* **MetricsNoData**: NoData alert<br><br>* **NoDataRecovered**: NoData alert recovery |Metric |* Render it directly: `{{ .Type }}`<br><br>* Use the extension function to translate it into natural language: `{{ translate "Type" "zh"  .Type }}`. For example, render `Metric` as `Alert` **.**  |
|SiteName |String |Site name. |Cloud Monitor |`{{ .SiteName }}` |
|AccountName |String |Account name. |user\-demo |`{{ .AccountName }}` |
|AccountId |String |Account ID. |21000\*\*\*\*\* |`{{ .AccountId }}` |
|RuleName |String |Alert policy name. |alert\-demo |`{{ .RuleName }}` |
|RuleId |String |Alert policy ID. |19251\*\*\*\*\* |`{{ .RuleId }}` |
|RuleURL |String |URL to the alert policy details. |https://console.byteplus.com/cloud\-monitor/alert/strategy?id=19251\*\*\*\*\*4565\*\*\*\*\* |`{{ .RuleURL }}` |
|RuleType |String |Alert policy type. Possible values:<br><br><br>* **static**: Static resources.<br><br>* **dynamic**: Dynamic resources.<br><br>* **account**: Account\-level metric alerts. |static |`{{ .RuleType }}` |
|Namespace |String |Namespace where the alert policy belongs. |VCM_ECS |* Render it directly: `{{ .Namespace }}`<br><br>* Use the extension function to translate it into natural language: `{{ translate "Namespace" "zh" .Namespace }}` |
|SubNamespace |String |Dimension where the metric belongs. |Instance |`{{ .SubNamespace }}` |
|Region |String |Region where the alert policy belongs. |cn\-beijing |* Render it directly: `{{ .Region }}`<br><br>* Use the extension function to translate into natural language: `{{ translate "Region" "zh" .Region }}`. For example, render `cn-beijing` as `China (Beijing)`. |
|HappenedAt |time.Time |The time when the alert is triggered. |2025\-01\-02 00:00:00(UTC+08:00) |Format the time: `{{ .HappenedAt.Format "2006-01-02 15:04:05(UTCZ07:00)" }}` |
|RuleCondition |String |Alert trigger condition. |Average QPS increased or decreased by 0% for 10 consecutive cycles compared to the previous cycle |`{{ .RuleCondition }}` |
|Level |String |Alert level. Possible values:<br><br><br>* **critical**<br><br>* **warning**<br><br>* **notice** |critical |* Render it directly: `{{ .Level }}`<br><br>* Use the extension function to translate into natural language: `{{ translate "Level" "zh" .Level }}`. For example, render `critical` as `Serious`. |
|ProjectName |String |Name of the project to which the alert policy belongs. |default |`{{ .Project }}` |
|TagSet |Array of Tag |Alert policy tags. Each tag consists of a `Key` and `Value`. |\- |Iterate through tags:<br><br>```Go```<br>```{{ range $idx, $tag := .Tags }}```<br>```{{ $tag.Key }}: {{ $tag.Value }}```<br>```{{ end }}```<br> |
|Resources |Array of ResourceMetric |A list of cloud product resources that triggered the alert. |\- |Iterate through resources:<br><br>```Go```<br>```{{ range $idx, $resource := .Resources }}```<br>```{{ $resource.Name }} ({{ $resource.Id}})```<br>```{{ end }}```<br> |
|HistoryURL |String |URL to the alert history page. |https://console.byteplus.com/cloud\-monitor/alert/history |`{{ .HistoryURL }}` |
|CreateSilenceURL |String |URL to creating an alert suppression policy. |https://console.byteplus.com/cloud\-monitor/notice/silencePolicy/create?ruleId=19251\*\*\*\*\* |`{{ .CreateSilenceURL }}` |


<span id="oXjJetf3"></span>
#### Tag


|Variable name |Type |Description |Sample value |Example |
|---|---|---|---|---|
|Key |String |Tag key. |test |`{{ $tag.Key }}` |
|Value |String |Tag value. |test |`{{ $tag.Value }}` |


<span id="3TkY91AP"></span>
#### ResourceMetric


|Variable name |Type |Description |Sample value |Example |
|---|---|---|---|---|
|AlertGroupId |String |Alert history ID. |67fd19\*\*\*\*\*\* |`{{ $resource.AlertGroupId }}` |
|AlertGroupURL |String |URL to the alert details of the cloud product resource. |https://console.byteplus.com/cloud\-monitor/alert/history/detail?id=67fd19\*\*\*\*\* |`{{ $resource.AlertGroupURL }}` |
|Id |String |Cloud product resource ID. |i\-yd9j\*\*\*\*\* |`{{ $resource.Id }}` |
|Name |String |Cloud product resource name. |ecs\-demo |`{{ $resource.Name }}` |
|DetailURL |String |URL to the cloud product resource monitor. |https://console.byteplus.com/cloud\-monitor/product/\*\*\*\*\*\*\* |`{{ $resource.DetailURL }}` |
|Region |String |Region where the cloud product resource belongs. |cn\-beijing |* Render it directly: `{{ $resource.Region }}`<br><br>* Use the extension function to translate into natural language: `{{ translate "Region" "zh" $resource.Region }}`. For example, render `cn-beijing` as `China (Beijing)`. |
|FirstAlertTime |time.Time |Time of the first alert occurrence. |2025\-01\-01 00:00:00(UTC+08:00) |Format the time: `{{ $resource.FirstAlertTime.Format "2006-01-02 15:04:05(UTCZ07:00)" }}` |
|LastAlertTime |time.Time |Time of last alert occurrence. |2025\-01\-02 00:00:00(UTC+08:00) |Format the time: `{{ $resource.LastAlertTime.Format "2006-01-02 15:04:05(UTCZ07:00)" }}` |
|LastSendLevel |String |Level of the last alert. Possible values:<br><br><br>* **critical**<br><br>* **warning**<br><br>* **notice**<br><br><br>This value is empty when the alert is sent for the first time. |warning |* Render it directly: `{{ .Level }}`<br><br>* Use the extension function to translate it into natural language: `{{ translate "Level" "zh" $resource.LastSendLevel }}`. For example, render `warning` as `warning`. |
|Metrics |Array of  MetricValue |A list of metrics configured in the alert policy.<br><br>When the value is `NaN`, it means no data. |\- |Iterate through metrics:<br><br>```Go```<br>```{{ range $idx, $metric := $resource.Metrics }}```<br>```{{ $metric.Name }}: {{ $metric.CurrentValue }}{{ $metric.Unit }}```<br>```{{ end }}```<br> |
|Dimensions |Array of MetricDimension |Dimensions of cloud product resources. |\- |Iterate through dimensions:<br><br>```Go```<br>```{{ range $idx, $dimension := $resource.Dimensions }}```<br>```{{ $dimension.Name }}: {{ $dimension.Value }}```<br>```{{ end }}```<br> |
|ProjectName |String |Name of the project to which the cloud product resource belongs. |default |`{{ $resource.ProjectName }}` |
|TagSet |Array of Tag |Resource tags of the cloud product. |\- |Iterate through tags:<br><br>```Go```<br>```{{ range $key, $val := $resource.Tags }}```<br>```{{ $key }}: {{ $val }}```<br>```{{ end }}```<br> |
|Metadatas |Array of Metadata |Metadata of the cloud product resource used for alerting. |\- |Iterate through metadata items:<br><br>```Go```<br>```{{ range $idx, $meta := $resource.Metadatas }}```<br>```{{ $meta.Name }}: {{ $meta.Value }}```<br>```{{ end }}```<br> |


<span id="sBIj8JTH"></span>
#### MetricValue


|Variable name |Type |Description |Sample value |Example |
|---|---|---|---|---|
|Name |String |The metric name. |CpuTotal |`{{ $metric.Name }}` |
|Unit |String |Threshold unit. |% |`{{ $metric.Unit }}` |
|Threshold |String |Metric threshold. |80 |`{{ $metric.Threshold }}` |
|CurrentValue |String |Current metric value. |90 |`{{ $metric.CurrentValue }}` |
|Descriptions |String |Metric description. |CPU utilization |`{{ $metric.Description }}` |
|Warn |Bool |Whether the metric meets the threshold condition. Available types:<br><br><br>* **true**: Meets the threshold.<br><br>* **false**: Does not meet the threshold. |true |`{{ $metric.Warn }}` |
|IsTimeCompare |Bool |Whether it is period\-over\-period or cycle\-on\-cycle comparison. Available types:<br><br><br>* **true**: Period\-over\-period comparison.<br><br>* **false**: Cycle\-on\-cycle comparison. |true |`{{ $metric.IsTimeCompare }}` |
|InherentUnit |String |Metric unit. |% |`{{ $metric.IsTimeCompare }}` |
|LastValue |String |Last metric value. |85 |`{{ $metric.LastValue }}` |
|LastDescription |String |Last metric description. The format is `{last cycle}/{same time yesterday}/{same time last week}{metric name}`. |CPU utilization of the last cycle |`{{ $metric.LastDescription }}` |
|CurrentValue |String |Current metric value. |91 |`{{ $metric.CurrentValue }}` |
|CurrentDescription |String |Current metric description. The format is `{current}{metric name}`. |Current CPU utilization |`{{ $metric.CurrentDescription }}` |


<span id="b3W8aumC"></span>
#### MetricDimension


|Variable name |Type |Description |Sample value |Example |
|---|---|---|---|---|
|Name |String |Cloud product dimension name. |ResourceID |`{{ $dimension.Name }}` |
|Value |String |Cloud product dimension value. |i\-yd9j\*\*\*\*\*ajrd7\*\*\*\*\* |`{{ $dimension.Value }}` |
|Description |String |Description of the cloud product dimension. |Instance ID |`{{ $dimension.Description }}` |


<span id="36k9Np1W"></span>
#### Metadata

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Different cloud products have different metadata items for alerting. Some cloud products may not have metadata that can be used in alerting.</div>



|Variable name |Type |Description |Sample value |Example |
|---|---|---|---|---|
|Name |String |Metadata name. |IP.Inside |`{{ $meta.Name }}` |
|Value |String |Metadata value. |192.168.0.1 |`{{ $meta.Value }}` |
|Descriptions |String |Dimension description. |Private IP address |`{{ $meta.Description }}` |


<span id="uecBWCgp"></span>
### Configuration example

In addition to the preset alerting templates of the system, you can specify custom content of a notification template based on the data structure of alert variables, Go template syntax, and Markdown syntax. The following section shows the configuration example.

```markdown
**Alert Information**:

---

Alert Type: {{ .Type }}
Account Name: {{ .AccountName }}
Account ID: {{ .AccountId }}
Alert Policy Name: {{ .RuleName }}
Alert Policy ID: {{ .RuleId }}
Alert Policy Details: {{ .RuleURL }}
Alert Policy Type: {{ .RuleType }}
Cloud Product Involved in Alert: {{ .Namespace }}
Cloud Product Dimension Involved in Alert: {{ .SubNamespace }}
Cloud Product Region: {{ .Region }}
Alert Occurrence Time: {{ .HappenedAt }}
Alert Trigger Condition: {{ .RuleCondition }}
Alert Level: {{ .Level }}
Link to Configure Alert Suppression Policy: {{ .CreateSilenceURL }}

---

**Details of Resources Triggering the Alert**:
{{- range $idx, $resource := .Resources }}
  Cloud Product Resource ID: {{- $resource.Id }}
  Cloud Product Resource Name: {{- $resource.Name }}
  Cloud Product Resource Region: {{- $resource.Region }}
  Cloud Product Resource Alert Details Link: {{- $resource.AlertGroupURL }}
  First Alert Occurrence Time: {{- $resource.FirstAlertTime }}
  Last Alert Occurrence Time: {{- $resource.LastAlertTime }}
  List of Metrics Configured in Alert Policy: {{ range $idx, $metric := $resource.Metrics }}
      Metric Name: {{ $metric.Name }}
      Threshold Unit: {{ $metric.Unit }}
      Metric Threshold: {{ $metric.Threshold }}
      Metric Current Value: {{ $metric.CurrentValue }}
      {{- end }}
{{- end }}
```


<span id="JMsaLwfs"></span>
## Event template variables

<span id="j5own9FE"></span>
### Data structure

The following JSON example demonstrates variables, parameters, and data structures supported in Cloud Monitor event templates. This helps you understand common Go template syntax and its usage.

```json
{
        "Type": "Event",
        "SiteName": "云监控",
        "AccountName": "user-demo",
        "AccountId": "21000*****",
        "Source": "ecs",
        "Level": "critical",
        "Id": "1803******",
        "Event": "ecs:Instance:RebootInstance.Executing",
        "HappenedAt": "2025-01-01 00:00:00(UTC+08:00)",
        "Region": "cn-beijing",
        "ResourceId": "i-yd9j*****",
        "ResourceName": "ecs-demo",
        "ProjectName": "default",
        "TagSet": [
          {
             "Key": "test",
             "Value": "test"
          }
        ],
        "Details": [
          {
             "id": "687f47006e921c57c64b79fb",
             "resourceid": "subnet-3rej6jce9fev45zs***",
             "source": "vpc"
          }
        ],
        "Rules": [
          {
             "RuleId": "19251*****",
             "RuleName": "event-demo",
             "Level": "critical",
             "RuleURL": "https://console.byteplus.com/cloud-monitor/event/rules/detail?id=1790****"
          }
        ], 
        "HistoryURL": "https://console.byteplus.com/cloud-monitor/alert/history"
}
```


<span id="AeVvGMPW"></span>
### Variable description

<div data-tips="true" data-tips-type="default">Descriptions</div>



* <div data-tips="true" data-tips-type="default">You can use the standard Go Template approach to get values of non\-nested variables. For example, you can use <code>{{ .Region }}</code>.</div>


* <div data-tips="true" data-tips-type="default">For nested vairables, you need to use custom variables to obtain all resources. For example, you define the <code>$rule</code> variable and use iteration to get all resources: <code>{{ range $idx, $rule := .Rules }}</code>. For internal variables, you need to use <code>$rule.fieldName </code>(for example, <code>{{ $rule.RuleId }}</code>) to get variable values.</div>



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
|HistoryURL |String |URL to the Event Center. |https://console.byteplus.com/cloud\-monitor/alert/history |`{{ .HistoryURL }}` |


<span id="cR5R1K32"></span>
#### EventRule


|Variable name |Type |Description |Sample value |Example |
|---|---|---|---|---|
|RuleId |String |Event rule ID. |19251\*\*\*\* |`{{ $rule.RuleId }}` |
|RuleName |String |Event rule name. |event\-demo |`{{ $rule.RuleName }}` |
|Level |String |Event rule level. Possible values:<br><br><br>* **critical**<br><br>* **warning**<br><br>* **notice** |critical |* Render it directly: `{{ $rule.Level }}`<br><br>* Use the extension function to translate into natural language: `{{ translate "Level" "zh" $rule.Level }}`. For example, render `critical` as `Serious`. |
|RuleURL |String |URL to the event rule. |https://console.byteplus.com/cloud\-monitor/event/rules/detail?id=1790\*\*\*\* |`{{ $rule.RuleURL }}` |


<span id="UPKcFaQy"></span>
### Configuration example

In addition to the preset event templates, you can specify custom content of a notification template based on the data structures of alert variables, Go Template syntax, and Markdown syntax. This section provides a configuration example.

```markdown
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

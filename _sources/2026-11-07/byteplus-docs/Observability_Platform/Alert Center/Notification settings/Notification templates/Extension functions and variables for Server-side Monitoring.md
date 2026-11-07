---
title: "Extension functions and variables for Server-side Monitoring"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Extension_functions_and_variables_for_Server-side_Monitoring"
---

You can use preset alert variables in notification templates. This topic describes the structure and parameters of preset alert variables for Server\-side Monitoring.

<span id="GzUtp1GI"></span>
## Extension functions

Server\-side Monitoring notification templates support Go Template built\-in functions and extension functions. The following table provides the details.


|**Function** |**Description** |
|---|---|
|Go Template built\-in functions |Notification templates support Go Template built\-in functions such as range, if, with, and len. For details, see the [official documentation](https://pkg.go.dev/text/template). |
|translate(typ, lang, val) |Convert values such as Type and Region into natural language. Example: `{{ translate "Type" "zh" .Type }}`. |
|levelColor(level, isRecovered) |Return the channel color value based on the severity level and whether the alert has recovered. Example: `{{ levelColor .Level false }}`. |
|levelCss(level, isRecovered) |Return a CSS class based on the severity level and whether the alert has recovered. Example: `{{ levelCss .Level false }}`. |
|formatKeyValues(kvs) |Format `[]KeyValues` into `k={v1,v2}` text. Example: `{{ formatKeyValues .Labels }}`. |
|getMetrics(typ, metrics) |Filter the metric list by alert type for better display. Example: `{{ range $m := getMetrics .Type $resource.Metrics }}`. |
|Time formatting |Fields of the `time.Time` type supports `.Format`. Example: `{{ .HappenedAt.Format "2006-01-02 15:04:05" }}`. |


<span id="jMsTnNyb"></span>
## Data structure

This topic uses the following JSON example to demonstrate the variables, parameters, and data structures included in Server\-side Monitoring alert information. This helps you understand common Go template syntax and its usage.

```JSON
{
  "Type": "Metric",
  "SiteName": "APMPlus",
  "AccountName": "AlertAccount",
  "AccountId": "210xxxxx7",
  "Region": "cn-beijing",
  "HappenedAt": "2026-06-24T21:23:25+08:00",
  "Level": "Fatal",
  "ProjectName": "default",
  "Domain": "",
  "MaxTitleLen": 512,
  "MaxContentLen": 16384,
  "MaxCount": 5,
  "LarkNotifyVerify": {
    "NeedVerify": false,
    "Timestamp": 0,
    "Sign": ""
  },
  "EmailFooterLogo": "volc_logo",
  "RuleName": "Alert",
  "RuleURL": "https://console.byteplus.com/observe/apmplus-server/region:apmplus-server+cn-beijing/server/alarm/detail?name=......%26rule_id=......",
  "RuleType": "Service Alert",
  "RuleDesc": "Template: Test Template, Rule: Test Rule, Application: ......",
  "CreateSilenceURL": "",
  "Workspace": "Test-Workspace",
  "RelatedServices": [
    "test1......",
    "test2-......"
  ],
  "Labels": [],
  "ContentsByCondition": [
    "Alert triggers when all the following conditions are met simultaneously",
    "Error Rate No filter conditions, aggregated by average grouped by [service], greater than ......% in the last 5 minutes"
  ],
  "Resources": [
    {
      "AlertGroupId": "69afbf........625ccb7",
      "Region": "cn-beijing",
      "ServiceName": "test1......",
      "ServiceMonitorURL": "",
      "FirstAlertTime": "2026-06-24T21:23:25+08:00",
      "LastAlertTime": "2026-06-24T21:23:25+08:00",
      "Metrics": [
        {
          "Name": "Error Rate",
          "Unit": "%",
          "Threshold": "......",
          "Value": "......",
          "Description": "Error Rate No filter conditions, aggregated by average grouped by [service], greater than ......% in the last 5 minutes",
          "Warn": true,
          "IsTimeCompare": false,
          "InherentUnit": "",
          "LastValue": "",
          "CurrentValue": "",
          "Index": 0,
          "DeltaValue": ""
        }
      ],
      "GroupBy": "{service = test1......}",
      "GroupByTags": [
        {
          "Key": "service",
          "Value": "test1......"
        }
      ]
    },
}
```


<span id="mCJPqHgK"></span>
## Variable description

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">You can use the standard Go Template approach to get values of non\-nested variables. For example, you can use <code>{{ .Region }}</code>.</div>


* <div data-tips="true" data-tips-type="default">For nested variables, you need to use custom variables to obtain all resources. For example, you define the <code>$resource</code> variable and use iteration to get all resources: <code>{{ range $idx, $resource := .Resources }}</code>. For internal variables, you need to use <code>$resource.fieldName</code> (for example, <code>{{ $resource.Id }}</code>) to get variable values.</div>



The following table provides the parameters and descriptions of preset variables that can be used in a notification template.


|**Variable name** |**Type** |**Description** |**Example** |**Example** |
|---|---|---|---|---|
|Type |string |The alarm type. Valid values: |Metric / MetricRecovered |{{ translate "Type" "zh" .Type }} |
|SiteName |string |Site name. |BytePlus |{{ .SiteName }} |
|AccountName |string |Account name. |test_user(12345) |{{ .AccountName }} |
|AccountId |string |Account ID. |21000\*\*\*\*\* |{{ .AccountId }} |
|Region |string |The region. |cn\-beijing |{{ translate "Region" "zh" .Region }} |
|HappenedAt |time.Time |The time when the alarm is triggered. |2025\-12\-01T00:00:00+08:00 |{{ .HappenedAt.Format "2006\-01\-02 15:04:05" }} |
|Level |string |The alert level. |critical |{{ .Level }} |
|ProjectName |string |The project name. |default |{{ .ProjectName }} |
|TagSet |[]Tag |The tag set. |[{Key:"service",Value:"test1"}] |{{ range .TagSet }}{{ .Key }}={{ .Value }} {{ end }} |
|Domain |string |The console domain name. |console.volcengine.com |{{ .Domain }} |
|MaxCount |int |The maximum number of resources displayed in the current channel. |5 |{{ .MaxCount }} |
|RuleName |string |Rule name. |Service alert test |{{ .RuleName }} |
|RuleURL |string |The URL of the rule details. |https://.../server/alarm/detail?... |[View the rule]({{ .RuleURL }}) |
|RuleType |string |The rule type text. |Service alert |{{ .RuleType }} |
|RuleDesc |string |Rule description. |Template: test template... |{{ .RuleDesc }} |
|CreateSilenceURL |string |The URL for creating a silence rule. |Empty string or URL |[Create a silence rule]({{ .CreateSilenceURL }}) |
|RelatedServices |[]string |The list of affected services. |["test1......", "test2\-......"] |{{ range .RelatedServices }}{{ . }} {{ end }} |
|Labels |[]KeyValues |The list of rule labels. |[] |{{ formatKeyValues .Labels }} |
|ContentsByCondition |[]string |The description of the trigger policy generated from the configured conditions. |An alert is triggered when all of the following conditions are met: |{{ range .ContentsByCondition }}{{ . }}\n{{ end }} |
|Resources |[]APMPlusResource |The list of alert resources. |2 service resources |{{ range $resource := .Resources }}{{ $resource.ServiceName }}{{ end }} |


<span id="Vq4anxC0"></span>
### Tag


|**Variable name** |**Type** |**Description** |**Example** |**Example** |
|---|---|---|---|---|
|Key |string |The tag key. |service |{{ $tag.Key }} |
|Value |string |The tag value. |test1...... |{{ $tag.Value }} |


<span id="P66uCh7Y"></span>
### KeyValues


|**Variable name** |**Type** |**Description** |**Example** |**Example** |
|---|---|---|---|---|
|Key |string |Tag key. |env |{{ $label.Key }} |
|Values |[]string |Multiple values under the same key. |["prod", "stg"] |{{ range $v := $label.Values }}{{ $v }} {{ end }} |


<span id="eitOzH2n"></span>
### APMPlusResource


|**Variable name** |**Type** |**Description** |**Example** |**Example** |
|---|---|---|---|---|
|AlertGroupId |string |The ID of the alert group. |69afbf........625ccb7 |{{ $resource.AlertGroupId }} |
|Region |string |The region where the resource is located. |cn\-beijing |{{ translate "Region" "zh" $resource.Region }} |
|ServiceName |string |The service name. |test1...... |{{ $resource.ServiceName }} |
|ServiceMonitorURL |string |The URL of the service monitoring details. |https://.../service/... |[Service monitoring]({{ $resource.ServiceMonitorURL }}) |
|FirstAlertTime |time.Time |The time of the first alert. |2025\-12\-01T00:00:00+08:00 |{{ $resource.FirstAlertTime.Format "2006\-01\-02 15:04:05" }} |
|LastAlertTime |time.Time |The time of the most recent alert. |2025\-12\-01T00:00:00+08:00 |{{ $resource.LastAlertTime.Format "2006\-01\-02 15:04:05" }} |
|Metrics |[]APMPlusMetricValue |The list of metrics for this resource. |1 error rate metric |{{ range $m := $resource.Metrics }}{{ $m.Name }}={{ $m.Value }}{{ end }} |
|GroupBy |string |The display string for resource aggregation. |{service = test1......} |{{ $resource.GroupBy }} |
|GroupByTags |[]Tag |The set of resource aggregation tags. |[{Key:"service",Value:"test1......"}] |{{ range $tag := $resource.GroupByTags }}{{ $tag.Key }}={{ $tag.Value }} {{ end }} |


<span id="H2WqWRi8"></span>
### APMPlusMetricValue


|**Variable name** |**Type** |**Description** |**Example** |**Example** |
|---|---|---|---|---|
|Name |string |The metric name. |Error rate |{{ $metric.Name }} |
|Unit |string |The display unit. |% |{{ $metric.Unit }} |
|Threshold |string |The threshold text. |...... |{{ $metric.Threshold }} |
|Value |string |The current value or rate of change. |...... |{{ $metric.Value }} |
|Description |string |Metric description. |Error rate, no filter conditions, aggregated by average... |{{ $metric.Description }} |
|Warn |bool |Whether it is an alert metric. |true |{{ $metric.Warn }} |
|IsTimeCompare |bool |Whether the metric uses a same\-period or sequential\-period comparison. |false |{{ $metric.IsTimeCompare }} |
|InherentUnit |string |The inherent unit of the metric. |empty string |{{ $metric.InherentUnit }} |
|LastValue |string |The previous window value. |Empty string |{{ $metric.LastValue }} |
|CurrentValue |string |The current window value. |Empty string |{{ $metric.CurrentValue }} |
|Index |int |The condition index. |0 |{{ $metric.Index }} |
|DeltaValue |string |The absolute change value. |Empty string |{{ $metric.DeltaValue }} |

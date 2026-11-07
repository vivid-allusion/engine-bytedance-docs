---
title: "Extension functions and variables for VMP"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Extension_functions_and_variables_for_VMP"
---

You can use preset alert variables in notification templates. This topic describes the structure and parameters of preset alert variables for VMP.

<span id="i5EnKpJE"></span>
## Extension functions

VMP notification templates support Go Template built\-in functions and extension functions. The following table provides the details.


|**Function** |**Description** |
|---|---|
|Go Template built\-in functions |Notification templates support Go Template built\-in functions such as range, if, with, and len. For details, see the [official documentation](https://pkg.go.dev/text/template). |
|translate(typ, lang, val) |Convert the variable value to natural language. In VMP scenarios, this function is most commonly used with the Region variable. For example: `{{ translate "Region" "zh" .Region }}`. |
|Time formatting |Fields of the `time.Time` type can directly use `.Format`. Example: `{{ .StartsAt.Format "2006-01-02 15:04:05" }}`. |
|Collection traversal |Collections such as `map[string]string` and `[]NotifyTemplateAlert` can be traversed using range. |
|vkeClusterName |Obtains a cluster name based on the `clusterID` of a Vital Kubernetes Engine (VKE) cluster. The VKE metrics written through the collection add\-on in a VKE cluster will contain the `cluster` label, whose value is the cluster ID. You can also use the extension function to obtain a cluster name in an alert notification. You can perform the following configuration to obtain the cluster name:<br><br><br>1. Ensure that the triggered alerts contain the `cluster` label. For example, you can use `sum(up)by(job,cluster)` to achieve aggregation by `cluster` when you configure alerts. In this case, the labels of the alerts will contain the `cluster` label.<br><br>2. When you configure an alert notification template, use the `vkeClusterName` function to obtain the cluster name. Line 4 of the following sample code shows how to obtain the endpoint name.<br><br><br>```Bash```<br>```{{ range $i, $alert := .Alerts -}}```<br>```{{ if lt $i 5 -}}```<br>```Resource No.{{ add1 $i }} {{ if $alert.Annotations }}：```<br>```ClusterName: {{ $alert.Labels.cluster \| vkeClusterName }}```<br>```{{- range $key, $value := $alert.Labels }}```<br>```{{ $key }}: {{ $value }}```<br>```{{- end }}```<br>```Current Value：{{ $alert.Value }}```<br>```Alert Event ID: {{ $alert.Id }}```<br>```Alert Start Time：{{ date "2006-01-02T15:04:05Z07:00" $alert.StartsAt }}```<br>``````<br>```---```<br>``````<br>```{{ else if eq $i 5 -}}```<br>```Only the first 5 faulty resource details are displayed. Click [Alert Event Details] ({{ $.AlertListConsoleURL }}) to view more```<br>```{{- end }}```<br>```{{- end }}```<br><br><br> |
|arkEndpointName |Obtains an endpoint name based on `endpointID`. The metrics written by ModelArk are all added with the `ark_endpoint` label, whose value is an endpoint ID. You can also use the extension function to obtain an endpoint name in an alert notification. You can perform the following configuration to obtain the endpoint name:<br><br><br>1. Ensure that the triggered alerts contain the `ark_endpoint` label. For example, you can use `sum by(ark_endpoint,api)(rate(ark_api_proxy_request_total{}[2m]))` to achieve aggregation by `ark_endpoint` when you configure alerts. In this case, the labels of the alerts will contain the `ark_endpoint` label.<br><br>2. When you configure an alert notification template, use the `arkEndpointName` function to obtain the endpoint name. Line 4 of the following sample code shows how to obtain the endpoint name.<br><br><br>```Bash```<br>```{{ range $i, $alert := .Alerts -}}```<br>```{{ if lt $i 5 -}}```<br>```Resource No.{{ add1 $i }}{{ if $alert.Annotations }}：```<br>```EndpointName: {{ $alert.Labels.ark_endpoint \| arkEndpointName }}```<br>```{{- range $key, $value := $alert.Labels }}```<br>```{{ $key }}: {{ $value }}```<br>```{{- end }}```<br>```Current Value：{{ $alert.Value }}```<br>```AlertID: {{ $alert.Id }}```<br>```Alert Start Time：{{ date "2006-01-02T15:04:05Z07:00" $alert.StartsAt }}```<br>``````<br>```---```<br>``````<br>```{{ else if eq $i 5 -}}```<br>```Only the first 5 faulty resource details are displayed. Click [Alert Event Details]({{ $.AlertListConsoleURL }}) to view more```<br>```{{- end }}```<br>```{{- end }}```<br><br><br> |
|last30minAlertDetailImageLarkKey |Obtain the image key of the alert flow chart for the last 30 minutes from the Feishu server. This extension function is only available for Feishu application bot notification templates.<br><br>```Bash```<br>```{{- $larkImageKey := last30minAlertDetailImageLarkKey }} {{if $larkImageKey }}```<br>```Alert Details in the Last 30 Minutes```<br>``` ![larkImage]({{$larkImageKey}}) {{end}}```<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Ensure that the Feishu application bot is updated to the latest version.</div><br> |
|last30minAlertDetailImageBase64 |Obtain the Base64 value of the alert flow chart image for the last 30 minutes. This extension function is only available for email notification templates.<br><br>```Bash```<br>```<img src="{{last30minAlertDetailImageBase64}}" alt="Image Description">```<br><br><br> |


<span id="uc3FdOKy"></span>
## Data structure

This topic demonstrates the variables, parameters, and data structure contained in the alert information of Vital Managed Service for Prometheus (VMP) by using the following sample JSON code. This helps you understand common Go template syntax and its usage.

```JSON
{
        "Region": "cn-beijing",
        "AlertingRuleName": "CPU usage is greater than 80%",
        "AlertingRuleDescription": "alarm description",
        "AlertingRuleDetailURL": "https://console.volcanicengine.com/prometheus/***3503d49e/detail",
        "Level": "P0",
        "PromQL": "rate(cpu_total[1m])",
        "Comparator": ">",
        "Threshold": "0.8",
        "For": "3m",
        "Alerts": [
          {
                  "Id": "cdwaihonj434390ad",
                  "Labels": {
                          "cluster": "ccmp26s0bjh01jhk860f0",
                          "namespace": "default",
                          "service": "nginx",
                          "pod": "nginx-85996***"
                  },
                  "Value": "0.84",
                  "StartsAt": "2024-02-02 17:13:32.065 +0800 CST",
                  "EndsAt": "2024-02-02 17:13:32.065 +0800 CST",
                  "DetailURL": "https://console.volcanicengine.com/prometheus/***/alert/alerting?detail_id=***"
                }
        ]
}
```


<span id="NVDEXjdT"></span>
## Variable description

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">You can use the standard Go Template approach to get values of non\-nested variables. For example, you can use <code>{{ .Region }}</code>.</div>


* <div data-tips="true" data-tips-type="default">For nested variables, you need to use custom variables to obtain all resources. For example, you define the <code>$resource</code> variable and use iteration to get all resources: <code>{{ range $idx, $resource := .Resources }}</code>. For internal variables, you need to use <code>$resource.fieldName</code> (for example, <code>{{ $resource.Id }}</code>) to get variable values.</div>



The following table provides the parameters and descriptions of preset variables that can be used in a notification template.


|**Variable name** |**Type** |**Description** |**Example** |**Example** |
|---|---|---|---|---|
|SiteName |string |Site name. |BytePlus |{{ .SiteName }} |
|Region |string |Region identifier |cn\-beijing |{{ translate "Region" "zh" .Region }} |
|AlertingStatus |string |Alert status. |firing |{{ .AlertingStatus }} |
|AlertingRuleName |string |Name of the alert rule. |test_template |{{ .AlertingRuleName }} |
|AlertingRuleDescription |string |The description of an alerting rule. |test custom template |{{ .AlertingRuleDescription }} |
|AlertingRuleDetailURL |string |The URL of the alert rule details page. |https://.../alert/rule/.../detail |[View the rule]({{ .AlertingRuleDetailURL }}) |
|AlertListConsoleURL |string |The URL of the alert list page. |https://.../alert/alerting?... |[View the alert list]({{ .AlertListConsoleURL }}) |
|SilencePolicyConsoleURL |string |The URL of the silence policy list page. |https://.../alert/silence |[View the silence policy]({{ .SilencePolicyConsoleURL }}) |
|GroupLabels |map[string]string |The aggregation labels of the current alert group. |{ "test": "1" } |{{ range $k, $v := .GroupLabels }}{{ $k }}={{ $v }} {{ end }} |
|CommonLabels |map[string]string |The labels shared by multiple alerts. |{ "test": "1" } |{{ range $k, $v := .CommonLabels }}{{ $k }}={{ $v }} {{ end }} |
|CommonAnnotations |map[string]string |The annotations shared by multiple alerts. |{ "test": "1" } |{{ range $k, $v := .CommonAnnotations }}{{ $k }}={{ $v }} {{ end }} |
|Level |string |The alert level. |P0 |{{ .Level }} |
|PromQL |string |The PromQL that triggers the current rule. |up{} |{{ .PromQL }} |
|Comparator |string |The comparator. |\> |{{ .Comparator }} |
|Threshold |float64 |The threshold of the alert. |0 |{{ .Threshold }} |
|For |string |The duration condition. |0s |{{ .For }} |
|Silence1hURL |string |The URL for a 1\-hour silence. |https://...silence_hours=1... |[Silence for 1 hour]({{ .Silence1hURL }}) |
|Alerts |[]Alert |The list of alert details in the current notification. |7 firing alerts |{{ range $alert := .Alerts }}{{ $alert.Id }}{{ end }} |


<span id="Q8Um6rRK"></span>
### Alert


|**Variable name** |**Type** |**Description** |**Example** |**Example** |
|---|---|---|---|---|
|Id |string |The ID of the alert details. |6842........6443........ |{{ range $alert := .Alerts }}{{ $alert.Id }}{{ end }} |
|Status |string |The status of the alert. |firing |{{ range $alert := .Alerts }}{{ $alert.Status }}{{ end }} |
|Labels |map[string]string |The labels of the alert. |{ "instance": "192.168...." } |{{ range $k, $v := $alert.Labels }}{{ $k }}={{ $v }} {{ end }} |
|Annotations |map[string]string |The annotations for the alert. |{ "test": "1" } |{{ range $k, $v := $alert.Annotations }}{{ $k }}={{ $v }} {{ end }} |
|Value |float64 |Current value. |1 |{{ $alert.Value }} |
|StartsAt |time.Time |The start time of the alert. |2025\-12\-01T00:00:00+08:00 |{{ $alert.StartsAt.Format "2006\-01\-02 15:04:05" }} |
|EndsAt |time.Time |The end time of the alert. It is typically a zero value when the alert has not recovered. |0001\-01\-01T00:00:00Z |{{ $alert.EndsAt.Format "2006\-01\-02 15:04:05" }} |
|DetailURL |string |The URL of the alert details page. |https://.../alert/alerting?detail_id=... |[View details]({{ $alert.DetailURL }}) |
|Fingerprint |string |The alert fingerprint. |................ |{{ $alert.Fingerprint }} |


<span id="dsY47Xs1"></span>
## Configuration example

In addition to the preset alert templates of the system, you can specify custom content of a message template based on the data structure of alert variables, Go Template syntax, and Markdown syntax. The following section shows the configuration example.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The details of failed resources are obtained through the <code>.Alerts.Labels</code> variable, and the value of the <code>Labels</code> parameter may vary based on different resources. In this example, parameters that contain <code>Labels.*</code> such as <code>$alert.Labels.instance</code>) are used for illustration only. In actual configuration, you need to specify the existing <code>Labels</code> variable of resources.</div>


* <div data-tips="true" data-tips-type="warning">If your notification template covers multiple resource types, you can also choose not to specify a <code>Label</code> variable and instead view the details of each failed resource. For the configuration method, refer to the <a href="https://docs.byteplus.com/en/docs/vmp/lark-alerting-notifacation-template#.5qih5p2_56S65L6L6K-05piO">Template example description</a> section of the Creating a notification template topic.</div>



```markdown
**Alert Information**：

---

Alert Region: {{ .Region }}
Alert Rule Name: {{ .AlertingRuleName }}
Alert Rule Description: {{ .AlertingRuleDescription }}
Alert Rule URL: {{ .AlertingRuleDetailURL }}
Alert Level: {{ .Level }}
PromQL Statement in Alert Rule: {{ .PromQL }}
Alert Comparison Condition: {{ .Comparator }}
Alert Threshold: {{ .Threshold }}
Alert Duration: {{ .For }}

---
{{- $alertCount := len .Alerts }}
{{- $maxAlerts := 10 }}

**Fault Resource Details ({{ $alertCount }} 个)**：
{{- range $idx, $alert := .Alerts }}
  {{- if lt $idx 10 }}
    {{- $labels := "" -}}
    <br>
    Fault Resource ID：{{- $alert.Id }}
    Fault Resource Cluster：{{- $alert.Labels.cluster }}
    Fault Resource Instance：{{- $alert.Labels.instance }}
    Fault Resource Job：{{- $alert.Labels.job }}
    Current Metric Value of Fault Resource：{{- $alert.Value }}
    Fault Start Time：{{- $alert.StartsAt }}
    Alert Event URL：{{- $alert.DetailURL}}
  {{- end }}
{{- end }}

---

{{- if gt $alertCount $maxAlerts }}
**The number of resources exceeds {{ $maxAlerts }}. Please go to the console to view complete alerts**.
{{- end }}
```
